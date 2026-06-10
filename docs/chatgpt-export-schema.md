# ChatGPT Export Findings

Sample analysed: `conversations-000.json`

## Sample Profile

* 100 conversations
* 1,342 graph nodes
* 1,235 messages on active conversation paths
* Date range: 29 May 2024 to 4 May 2026
* 410 user messages and 617 assistant messages on active paths
* 7 attachment records

The numbered filename may represent one chunk of a larger export. A complete
import should discover and combine all `conversations-*.json` files.

## Useful Structure

The file is an array of conversation objects.

```text
conversation
├── id / conversation_id
├── title
├── create_time
├── update_time
├── current_node
└── mapping
    └── <node id>
        ├── id
        ├── parent
        └── message
            ├── id
            ├── author.role
            ├── create_time
            ├── content
            └── metadata
```

`mapping` is a graph keyed by node ID. Nodes contain a `parent` reference but
no `children` array in this sample.

Each conversation has one root placeholder whose `message` is `null`.

## Reconstructing a Conversation

Use the selected branch, rather than every node in `mapping`:

1. Start at `current_node`.
2. Follow each node's `parent` until `null`.
3. Reverse the result to restore conversation order.
4. Ignore the root node with a null message.

Four conversations in the sample contain branches. Seven messages are outside
the selected paths and appear to be superseded alternatives. Reading all
mapping values would include these messages and can duplicate or contradict
the visible conversation.

Do not use timestamps alone to order messages. The sample contains generated
assistant and tool sequences whose timestamps do not follow their graph order.

## Report-Worthy Data

### Primary evidence

* User text: `message.content.parts[]` for `text` and `multimodal_text`
* Message time: `message.create_time` as Unix seconds
* Conversation time range: `create_time` and `update_time`
* Conversation title: useful as an index or topic hint, but not evidence alone
* Attachment metadata: `metadata.attachments[]`

User messages are the strongest evidence of interests, projects, questions,
intentions, and change over time.

### Supporting context

* Assistant `text` responses can clarify what the user was working through.
* Assistant claims should not be treated as facts about the user unless the
  user's messages support them.

### Usually exclude

* `system` and `tool` messages
* Browsing displays, quotes, execution output, and system errors
* Model, serialization, citation, and UI metadata
* Inactive branch nodes

These fields describe ChatGPT's operation more than the user's history.

## Content Variants

The sample contains these content types:

* `text`: text is stored in `content.parts`
* `multimodal_text`: `parts` mixes text strings with image-reference objects
* `code`: code is stored in `content.text`, with `content.language`
* Tool-specific types: browsing results, quotes, execution output, and errors

Seven messages include attachment metadata: six images and one CSV. The JSON
describes these files but does not necessarily contain their full contents, so
attachment analysis depends on the corresponding exported files being
available.

## Minimal Extraction Record

For report generation, reduce each selected message to:

```json
{
  "conversation_id": "...",
  "conversation_title": "...",
  "message_id": "...",
  "timestamp": 0,
  "role": "user",
  "text": "...",
  "attachments": []
}
```

Preserve IDs for traceability, but send only the fields needed for analysis to
the reporting prompt.

## Practical Conclusion

The export contains enough structured data for Footprints. The important work
is not decoding the schema; it is selecting the active branch, extracting
user-authored text consistently, preserving chronology, and preventing
assistant or tool output from being mistaken for evidence about the user.
