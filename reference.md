# Reference
## Accounts
<details><summary><code>client.Accounts.List() -> *pylon.GetAccountsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of accounts for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsListRequest{}
client.Accounts.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of accounts to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Create(request) -> *pylon.CreateAccountResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new account with the specified name and optional metadata.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsCreateRequest{
    Name: "name",
}
client.Accounts.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountType:** `*pylon.CreateAccountRequestAccountType` — The type of the account. Must be one of "customer", "internal", "community", or "partner". Defaults to "customer" if not specified.
    
</dd>
</dl>

<dl>
<dd>

**channels:** `[]*pylon.Channel` — An array of channels to be linked to this account.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this account.
    
</dd>
</dl>

<dl>
<dd>

**domain:** `*string` — Deprecated. Please use Domains and PrimaryDomain instead.
    
</dd>
</dl>

<dl>
<dd>

**domains:** `[]string` — The domains of the account, without any leading scheme, for example stripe.com. Must specify one domain as primary.
    
</dd>
</dl>

<dl>
<dd>

**externalIDs:** `[]*pylon.ExternalID` — An array of external IDs to be used on this account. If provided, the account's external IDs will be updated to the given external IDs.
    
</dd>
</dl>

<dl>
<dd>

**logoURL:** `*string` — The logo URL of the account. Must be a square .png, .jpg or .jpeg.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — The name of the account.
    
</dd>
</dl>

<dl>
<dd>

**ownerID:** `*string` — The ID of the owner of the account.
    
</dd>
</dl>

<dl>
<dd>

**primaryDomain:** `*string` — Must be in the list of domains. If there are any domains, there must be exactly one primary domain.
    
</dd>
</dl>

<dl>
<dd>

**subaccountIDs:** `[]string` — An array of account IDs to be added as subaccounts to this account. For normal accounts, these represent subaccounts. For partner accounts, these represent associated accounts.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — An array of strings to use as tags on this account. If provided, the accounts tags will be updated to the given tags.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.BulkUpdate(request) -> *pylon.UpdateAccountsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates multiple accounts in a single request. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsBulkUpdateRequest{
    AccountIDs: []string{
        "account_ids",
    },
}
client.Accounts.BulkUpdate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountIDs:** `[]string` — The account IDs to update. The number of accounts to update must be between 1 and 100.
    
</dd>
</dl>

<dl>
<dd>

**accountType:** `*pylon.UpdateAccountsRequestAccountType` — The type of the account. Can only be changed to "customer" or "partner".
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be updated on the accounts.
    
</dd>
</dl>

<dl>
<dd>

**isDisabled:** `*bool` — Whether the accounts are disabled.
    
</dd>
</dl>

<dl>
<dd>

**ownerID:** `*string` — The ID of the new owner. If empty string is passed in, the owner will be removed.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — An array of tags to be updated on the accounts.
    
</dd>
</dl>

<dl>
<dd>

**tagsApplyMode:** `*pylon.UpdateAccountsRequestTagsApplyMode` — The mode for applying tags. Valid values: "append_only", "remove_only", "replace". Defaults to "replace".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Merge(request) -> *pylon.MergeAccountsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Merges one or more accounts into a surviving account. Issues, contacts, opportunities, domains, channels, external IDs, and other associated data are transferred to the surviving account. Tags and custom field values of the merged accounts are not transferred. The merged accounts are permanently deleted. This cannot be undone. Accounts are merged sequentially, each in its own transaction; if a merge fails partway through, accounts already merged are not restored.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsMergeRequest{
    MergeAccountIDs: []string{
        "merge_account_ids",
    },
    MergeIntoAccountID: "merge_into_account_id",
}
client.Accounts.Merge(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mergeAccountIDs:** `[]string` — The IDs of the accounts to merge into the surviving account. These accounts are permanently deleted after their data is transferred. The number of accounts to merge must be between 1 and 100.
    
</dd>
</dl>

<dl>
<dd>

**mergeIntoAccountID:** `string` — The ID of the account that will survive the merge and receive the merged data.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Search(request) -> *pylon.SearchAccountsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Optionally pass `search_text` for fuzzy matching. Results are intersected with any provided filter.

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `id` | `equals`, `in`, `not_in` |
 `domains` | `contains`, `does_not_contain`, `in`, `not_in` |
 `tags` | `contains`, `does_not_contain`, `in`, `not_in` |
 `name` | `equals`, `in`, `not_in`, `string_contains` |
 `external_ids` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `owner_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |

For custom fields, pass the field slug as `field`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsSearchRequest{}
client.Accounts.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of accounts to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>

<dl>
<dd>

**searchText:** `*string` — Fuzzy text search. Results are intersected with any provided filter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Get(ID) -> *pylon.GetAccountResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single account by ID or external ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsGetRequest{
    ID: "id",
}
client.Accounts.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the account to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Delete(ID) -> *pylon.DeleteAccountResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes an account by ID or external ID.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsDeleteRequest{
    ID: "id",
}
client.Accounts.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the account to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Update(ID, request) -> *pylon.UpdateAccountResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing account by ID or external ID. Only provided fields are modified.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsUpdateRequest{
    ID: "id",
}
client.Accounts.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the account to update.
    
</dd>
</dl>

<dl>
<dd>

**accountType:** `*pylon.UpdateAccountRequestBodyAccountType` — The type of the account. Can only be changed to "customer" or "partner".
    
</dd>
</dl>

<dl>
<dd>

**channels:** `[]*pylon.Channel` — An array of channels to be linked to this account. If provided, replaces the account's linked channels; channels you leave out are unlinked.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this account.
    
</dd>
</dl>

<dl>
<dd>

**domains:** `[]string` — Domains of the account. Replaces the account's domains. Must specify one domain as primary.
    
</dd>
</dl>

<dl>
<dd>

**externalIDs:** `[]*pylon.ExternalID` — An array of external IDs to be used on this account. If provided, the account's external IDs will be updated to the given external IDs.
    
</dd>
</dl>

<dl>
<dd>

**isDisabled:** `*bool` — Whether the account is disabled.
    
</dd>
</dl>

<dl>
<dd>

**logoURL:** `*string` — Logo URL of the account.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the account.
    
</dd>
</dl>

<dl>
<dd>

**ownerID:** `*string` — The ID of the owner of the account. If empty string is passed in, the owner will be removed.
    
</dd>
</dl>

<dl>
<dd>

**primaryDomain:** `*string` — Must be in the list of domains. If there are any domains, there must be exactly one primary domain.
    
</dd>
</dl>

<dl>
<dd>

**subaccountIDs:** `[]string` — An array of account IDs to set as this account's subaccounts. If provided, the account's subaccounts become exactly this list; accounts you leave out are detached.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — An array of strings to use as tags on this account. If provided, the accounts tags will be updated to the given tags.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.UploadFile(AccountID, request) -> *pylon.UploadAccountFileResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads one or more files to an account by ID or external ID.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AccountsUploadFileRequest{
    AccountID: "id",
    File: strings.NewReader(
        "",
    ),
}
client.Accounts.UploadFile(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account to upload files to.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ActivityTypes
<details><summary><code>client.ActivityTypes.List() -> *pylon.GetActivityTypesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all custom activity type definitions for the organization.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.ActivityTypes.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ArticleFeedback
<details><summary><code>client.ArticleFeedback.List() -> *pylon.GetArticleFeedbackResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of knowledge base article feedback for the organization.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ArticleFeedbackListRequest{}
client.ArticleFeedback.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of feedback submissions to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>

<dl>
<dd>

**knowledgeBaseID:** `*string` — The ID of the knowledge base to filter by.
    
</dd>
</dl>

<dl>
<dd>

**articleID:** `*string` — The ID of the article to filter by.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Attachments
<details><summary><code>client.Attachments.Create(request) -> *pylon.CreateAttachmentResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads a file as an attachment. Send either `file` or `file_url` (`file` takes precedence if both are sent); one file per request. Executable and script files are rejected. The returned `url` is a signed link; pass it in `attachment_urls` when creating issues or messages. Files up to 100 MB (104,857,600 bytes) are supported. Larger files may be rejected and should be shared using an externally hosted link. This applies to direct uploads and files fetched through file_url. Downstream delivery channels may impose smaller limits.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AttachmentsCreateRequest{
    File: strings.NewReader(
        "",
    ),
}
client.Attachments.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## AuditLogs
<details><summary><code>client.AuditLogs.List() -> *pylon.GetAuditLogsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of audit log entries for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AuditLogsListRequest{}
client.AuditLogs.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of audit logs to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.AuditLogs.Search(request) -> *pylon.GetAuditLogsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a filtered, paginated list of audit log entries for the organization.
Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `action` | `equals`, `in`, `not_in`, `string_contains`, `string_does_not_contain` |
 `action_happened_at` | `time_is_after`, `time_is_before`, `time_range` |
 `object_id` | `equals`, `in`, `not_in` |

Timestamp values use RFC3339 format. `object_id` is the ID of the object the entry is
for, matching the `object_id` field of the returned entries.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.AuditLogsSearchRequest{}
client.AuditLogs.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of audit logs to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CallRecordings
<details><summary><code>client.CallRecordings.Create(request) -> *pylon.CreateCallRecordingResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a call recording from your own call recorder. Set app_type to `custom_call_recorder`; the Custom Call Recorder integration must be enabled for your organization, or the request returns 400. start_time, end_time, and at least one call_recording_messages entry are required. Every speaker_email must appear in participant_emails or match primary_user_email. The recording is linked to account_id if provided, otherwise to an account matched from the participant emails. Reusing a recording_id returns the existing recording unchanged.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CallRecordingsCreateRequest{
    AppType: pylon.CreateCallRecordingRequestAppTypeCustomCallRecorder,
    CallRecordingMessages: []*pylon.CreateCallRecordingMessageRequest{
        &pylon.CreateCallRecordingMessageRequest{
            MessageContent: "message_content",
        },
    },
    EndTime: pylon.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
    StartTime: pylon.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
}
client.CallRecordings.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `*string` — The ID of the account to link this call recording to. If provided, the participant emails are not used for account matching, and an unknown ID returns 400. If omitted, Pylon matches an account from the participant emails, ignoring your organization's own domains; the recording is created without an account if none matches.
    
</dd>
</dl>

<dl>
<dd>

**appType:** `pylon.CreateCallRecordingRequestAppType` — The source of the recording. Must be `custom_call_recorder`, which requires the Custom Call Recorder integration to be enabled.
    
</dd>
</dl>

<dl>
<dd>

**callRecordingMessages:** `[]*pylon.CreateCallRecordingMessageRequest` — The transcript, one entry per utterance. `custom_call_recorder` takes its transcript only from this field and ignores a plain-text transcript.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — Custom fields to set on the call recording. Use slugs from GET /custom-fields?object_type=meeting. Each entry needs a slug and either value or values, not both.
    
</dd>
</dl>

<dl>
<dd>

**endTime:** `time.Time` — When the call ended, in RFC3339 format (e.g. 2025-01-01T01:00:00Z).
    
</dd>
</dl>

<dl>
<dd>

**participantEmails:** `*string` — Comma-separated emails of everyone on the call (e.g. "alice@customer.com,bob@yourcompany.com"). Used to match the account when account_id is omitted. Every speaker_email in call_recording_messages must be in this list or match primary_user_email.
    
</dd>
</dl>

<dl>
<dd>

**primaryUserEmail:** `*string` — The email of the Pylon user who owns the recording. Counted as a participant, so it does not need to be repeated in participant_emails.
    
</dd>
</dl>

<dl>
<dd>

**recordingID:** `*string` — Your unique ID for this recording. Pylon deduplicates on recording_id and app_type: a request that reuses a recording_id returns the existing recording unchanged. Send a unique value for every call; if you omit it, every request after the first returns the same recording.
    
</dd>
</dl>

<dl>
<dd>

**recordingURL:** `*string` — A link to the recording in your call recorder. Maximum 255 characters.
    
</dd>
</dl>

<dl>
<dd>

**startTime:** `time.Time` — When the call started, in RFC3339 format (e.g. 2025-01-01T00:00:00Z).
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — The title of the call recording.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CallRecordings.Search(request) -> *pylon.SearchCallRecordingsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `account_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `source` | `equals`, `in`, `not_in` |
 `title` | `equals`, `string_contains` |
 `start_time` | `time_is_after`, `time_is_before`, `time_range` |

Timestamp values use RFC3339 format.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CallRecordingsSearchRequest{}
client.CallRecordings.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of call recordings to fetch. Defaults to 100. Must be greater than 0 and less than or equal to 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CallRecordings.Get(ID) -> *pylon.GetCallRecordingResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single call recording by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CallRecordingsGetRequest{
    ID: "id",
}
client.CallRecordings.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the call recording to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CallRecordings.Delete(ID) -> *pylon.DeleteCallRecordingResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a call recording by its Pylon ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CallRecordingsDeleteRequest{
    ID: "id",
}
client.CallRecordings.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The Pylon ID of the call recording to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CallRecordings.Update(ID, request) -> *pylon.UpdateCallRecordingResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a call recording by ID. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CallRecordingsUpdateRequest{
    ID: "id",
}
client.CallRecordings.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the call recording to update.
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `*string` — The account ID to associate with the call recording. Pass an empty string to remove the account association.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to set on the call recording. Only passed in fields will be modified.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Contacts
<details><summary><code>client.Contacts.List() -> *pylon.GetContactsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of contacts for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsListRequest{}
client.Contacts.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of contacts to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Contacts.Create(request) -> *pylon.CreateContactResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new contact with the specified email and optional metadata.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsCreateRequest{
    Name: "name",
}
client.Contacts.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountExternalID:** `*string` — The external ID of the account that this contact belongs to. Cannot be used together with account_id.
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `*string` — The account that this contact belongs to.
    
</dd>
</dl>

<dl>
<dd>

**avatarURL:** `*string` — The avatar URL of the contact. Must be a square .png, .jpg or .jpeg.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be applied to this contact.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — The email of the contact.
    
</dd>
</dl>

<dl>
<dd>

**externalIDs:** `[]*pylon.ExternalID` — An array of external IDs to be used on this contact.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — The name of the contact.
    
</dd>
</dl>

<dl>
<dd>

**phoneNumbers:** `[]string` — The phone numbers of the contact. Must contain only digits 0-9, optionally preceded by + (E.164, e.g. +4365446231), and be 15 digits or less. Include the + and country code for non-US numbers; a 10-digit number without + is treated as US.
    
</dd>
</dl>

<dl>
<dd>

**portalRole:** `*string` 

The portal role to assign to the contact. If not provided uses the default portal role from the portal settings.

Known values: `no_access`, `member`, `admin`. This list is not exhaustive.
    
</dd>
</dl>

<dl>
<dd>

**portalRoleID:** `*string` — The ID of the custom portal role to assign to the contact. Takes precedence over portal_role if provided.
    
</dd>
</dl>

<dl>
<dd>

**primaryPhoneNumber:** `*string` — The primary phone number. Must be in the list of phone_numbers. If there are any phone_numbers and this is not specified, the first phone number will be primary.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Contacts.Search(request) -> *pylon.SearchContactsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `id` | `equals`, `in`, `not_in` |
 `email` | `equals`, `in`, `not_in`, `string_contains` |
 `name` | `equals`, `in`, `not_in`, `string_contains` |
 `account_id` | `equals`, `in`, `not_in` |

For custom fields, pass the field slug as `field`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsSearchRequest{}
client.Contacts.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of contacts to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>

<dl>
<dd>

**searchText:** `*string` — Text search across contact name, primary email, secondary emails, primary phone number, and secondary phone numbers. Results are intersected with any provided filter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Contacts.Get(ID) -> *pylon.GetContactResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single contact by ID or external ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsGetRequest{
    ID: "id",
}
client.Contacts.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the contact.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Contacts.Delete(ID) -> *pylon.DeleteContactResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a contact by ID or external ID.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsDeleteRequest{
    ID: "id",
}
client.Contacts.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the contact to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Contacts.Update(ID, request) -> *pylon.UpdateContactResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a contact by ID or external ID. Only provided fields are modified.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ContactsUpdateRequest{
    ID: "id",
}
client.Contacts.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or external ID of the contact to update.
    
</dd>
</dl>

<dl>
<dd>

**accountExternalID:** `*string` — The external ID of the account to move the contact to. Cannot be used together with account_id.
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `*string` — The account to move the contact to. If empty string is passed in, the contact will be removed from its account.
    
</dd>
</dl>

<dl>
<dd>

**avatarURL:** `*string` — The avatar URL of the contact. Must be a square .png, .jpg or .jpeg.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be applied to this contact.
    
</dd>
</dl>

<dl>
<dd>

**email:** `*string` — The email of the contact. Replaces all of the contact's emails with this single email. Cannot be used together with the `emails` array field.
    
</dd>
</dl>

<dl>
<dd>

**emails:** `[]*pylon.UpdateContactEmail` 

The emails of the contact as an array. Cannot be used together with the singular `email` field.
Each entry must include an `email` string and an optional `is_primary` boolean.
If no email is marked as primary, the first email becomes the primary.
    
</dd>
</dl>

<dl>
<dd>

**externalIDs:** `[]*pylon.ExternalID` — An array of external IDs to be used on this contact. If provided, the contact's external IDs will be updated to the given external IDs.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 

in: body
The name of the contact.
    
</dd>
</dl>

<dl>
<dd>

**phoneNumbers:** `[]string` — The phone numbers of the contact. Must contain only digits 0-9, optionally preceded by + (E.164, e.g. +4365446231), and be 15 digits or less. Include the + and country code for non-US numbers; a 10-digit number without + is treated as US.
    
</dd>
</dl>

<dl>
<dd>

**portalRole:** `*string` 

The portal role to assign to the contact. Can be one of `no_access`, `member`, or `admin`, or a custom role slug.

Known values: `no_access`, `member`, `admin`. This list is not exhaustive.
    
</dd>
</dl>

<dl>
<dd>

**portalRoleID:** `*string` — The ID of the custom portal role to assign to the contact. Takes precedence over portal_role if provided.
    
</dd>
</dl>

<dl>
<dd>

**primaryPhoneNumber:** `*string` — The primary phone number. Must be in the list of phone_numbers. If there are any phone_numbers and this is not specified, the first phone number will be primary.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CustomFields
<details><summary><code>client.CustomFields.List() -> *pylon.GetCustomFieldsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all custom field definitions for the specified object type. Use `slug` (and `select_metadata.options[].slug` for option values) in API writes and filters.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomFieldsListRequest{
    ObjectType: pylon.ListCustomFieldsRequestObjectTypeAccount,
}
client.CustomFields.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**objectType:** `pylon.ListCustomFieldsRequestObjectType` — The object type of the custom fields. Can be "account", "issue", "contact", "task", "project", "meeting", or "opportunity".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomFields.Create(request) -> *pylon.CreateCustomFieldResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new custom field definition for the specified object type.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomFieldsCreateRequest{
    Label: "label",
    ObjectType: pylon.CreateCustomFieldRequestBodyObjectTypeAccount,
    Type: "text",
}
client.CustomFields.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**defaultValue:** `*string` — The default value for single-valued custom fields.
    
</dd>
</dl>

<dl>
<dd>

**defaultValues:** `[]string` — The default values for multi-valued custom fields.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — The description of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**label:** `string` — The label of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**objectType:** `pylon.CreateCustomFieldRequestBodyObjectType` — The object type of the custom field. Can be "account", "issue", "contact", "task", "project", "meeting", or "opportunity".
    
</dd>
</dl>

<dl>
<dd>

**selectOptions:** `[]*pylon.CustomFieldDefinitionSelectOption` — The list options of the select custom field. This is only present for select and multiselect custom fields.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — The slug of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**type_:** `string` — The type of the custom field. Can be one of `text`, `number`, `decimal`, `boolean`, `date`, `datetime`, `user`, `url`, `select`, or `multiselect`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomFields.Get(ID) -> *pylon.GetCustomFieldResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single custom field definition by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomFieldsGetRequest{
    ID: "id",
}
client.CustomFields.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the custom field.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomFields.Update(ID, request) -> *pylon.UpdateCustomFieldResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a custom field definition. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomFieldsUpdateRequest{
    ID: "id",
}
client.CustomFields.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**defaultValue:** `*string` — The default value for single-valued custom fields.
    
</dd>
</dl>

<dl>
<dd>

**defaultValues:** `[]string` — The default values for multi-valued custom fields.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — The description of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**label:** `*string` — The label of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**selectOptions:** `[]*pylon.CustomFieldDefinitionSelectOption` — The complete list of options for a select or multiselect custom field. Options missing from the list are deleted and their stored values are cleared asynchronously. Prefer the dedicated select option endpoints, which can rename an option without losing stored values.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — The slug of the custom field.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CustomObjects
<details><summary><code>client.CustomObjects.List(Type) -> *pylon.GetCustomObjectsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns paginated custom objects of the given type.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsListRequest{
    Type: "type",
}
client.CustomObjects.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — Pagination cursor for the next page.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — Number of results per page. Defaults to 25, max 100.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.Create(Type, request) -> *pylon.CreateCustomObjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new custom object instance of the given type. To link the object to an account, pass the built-in Account relationship field in `custom_fields`: `{"name":"Example","custom_fields":{"account":{"value":"account_uuid"}}}`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsCreateRequest{
    Type: "type",
    Name: "name",
}
client.CustomObjects.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `map[string]*pylon.CustomFieldValue` — Custom field values to set on the object, keyed by field slug. To link the object to an account, pass the built-in Account relationship field as `custom_fields.account.value`, for example `{"custom_fields":{"account":{"value":"account_uuid"}}}`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — The name of the custom object.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.BulkUpdate(Type, request) -> *pylon.UpdateCustomObjectsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies the same update to multiple custom objects of the given type in a single request. Pass between 1 and 100 IDs and the custom field values to set; only the provided fields are modified on each object. To update the linked account, pass the built-in Account relationship field in `custom_fields`: `{"ids":["object_uuid"],"custom_fields":{"account":{"value":"account_uuid"}}}`. To unset a field, pass its slug with an empty value.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsBulkUpdateRequest{
    Type: "type",
    IDs: []string{
        "ids",
    },
}
client.CustomObjects.BulkUpdate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "opportunity").
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `map[string]*pylon.CustomFieldValue` — Custom field values to apply to every listed custom object, keyed by field slug. To unset a field, pass its slug with an empty value.
    
</dd>
</dl>

<dl>
<dd>

**ids:** `[]string` — The IDs of the custom objects to update. Must be between 1 and 100 IDs.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.Search(Type, request) -> *pylon.SearchCustomObjectsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `name` | `equals`, `in`, `not_in`, `string_contains`, `string_does_not_contain`, `is_set`, `is_unset` |
 `account` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |

`account` is the built-in Account relationship field present on every custom object type; its values are account IDs.
Timestamp values use RFC3339 format. For custom fields, pass the field slug as `field`.

A `{type}` of `opportunity` is an alias for the opportunities API and filters on a different set of fields:

 Field | Allowed operators |
 --- | --- |
 `name` | `equals`, `in`, `not_in`, `string_contains` |
 `account_id` | `equals`, `in`, `not_in` |
 `source` | `equals`, `in`, `not_in` |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsSearchRequest{
    Type: "type",
}
client.CustomObjects.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of results to fetch. Defaults to 25, max 100.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.Get(Type, ID) -> *pylon.GetCustomObjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single custom object by ID, including its custom field values.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsGetRequest{
    Type: "type",
    ID: "id",
}
client.CustomObjects.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**id:** `string` — The ID of the custom object.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.Delete(Type, ID) -> *pylon.DeleteCustomObjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a custom object instance.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsDeleteRequest{
    Type: "type",
    ID: "id",
}
client.CustomObjects.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**id:** `string` — The ID of the custom object.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomObjects.Update(Type, ID, request) -> *pylon.UpdateCustomObjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates a custom object. Only provided fields are modified. To update the linked account, pass the built-in Account relationship field in `custom_fields`: `{"custom_fields":{"account":{"value":"account_uuid"}}}`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.CustomObjectsUpdateRequest{
    Type: "type",
    ID: "id",
}
client.CustomObjects.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type_:** `string` — The type slug of the custom object (e.g. "companies").
    
</dd>
</dl>

<dl>
<dd>

**id:** `string` — The ID of the custom object.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `map[string]*pylon.CustomFieldValue` — Custom field values to set on the object, keyed by field slug. To update the linked account, pass the built-in Account relationship field as `custom_fields.account.value`, for example `{"custom_fields":{"account":{"value":"account_uuid"}}}`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the custom object.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## EmailSuppressions
<details><summary><code>client.EmailSuppressions.List() -> *pylon.GetEmailSuppressionsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the email addresses Pylon will not send to, most recently suppressed first. Pass `email` to check a single address; an empty `data` array means it is not suppressed.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.EmailSuppressionsListRequest{}
client.EmailSuppressions.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**email:** `*string` — Only return the suppression for this email address, if one exists.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of suppressions to fetch. Defaults to 100. Must be greater than 0 and less than or equal to 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.EmailSuppressions.Delete(ID) -> *pylon.DeleteEmailSuppressionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the suppression so Pylon resumes sending email to the address.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.EmailSuppressionsDeleteRequest{
    ID: "id",
}
client.EmailSuppressions.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the email suppression to remove.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## FeatureRequests
<details><summary><code>client.FeatureRequests.Create(request) -> *pylon.CreateFeatureRequestResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new feature request. When should_auto_fetch_evidence is true, supporting evidence is automatically gathered and used to generate the description.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsCreateRequest{
    Title: "title",
}
client.FeatureRequests.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**description:** `*string` — The description of the feature request. Ignored when should_auto_fetch_evidence is true, since the description is then generated from gathered evidence.
    
</dd>
</dl>

<dl>
<dd>

**shouldAutoFetchEvidence:** `*bool` — When true, asynchronously gathers supporting evidence and generates a description, mirroring the in-app experience. Defaults to false, which creates the feature request as-is.
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — The title of the feature request.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.Merge(request) -> *pylon.MergeFeatureRequestsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Merges one or more feature requests into a surviving feature request. Evidence and linked external issues are consolidated, and merged feature requests are archived. Merge requests that share a target should be sent serially.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsMergeRequest{
    MergeFeatureRequestIDs: []string{
        "merge_feature_request_ids",
    },
    MergeIntoFeatureRequestID: "merge_into_feature_request_id",
}
client.FeatureRequests.Merge(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mergeFeatureRequestIDs:** `[]string` — The IDs of the Feature Requests to merge into the surviving Feature Request. Must contain between 1 and 100 unique IDs.
    
</dd>
</dl>

<dl>
<dd>

**mergeIntoFeatureRequestID:** `string` — The ID of the Feature Request that will survive the merge.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.Search(request) -> *pylon.SearchFeatureRequestsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns feature requests matching the given criteria. Supports semantic search, status filtering, and pagination.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsSearchRequest{}
client.FeatureRequests.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountIDs:** `[]string` — Filter by one or more account IDs. Returns only feature requests with evidence linked to any of the given accounts.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The maximum number of feature requests to return. Defaults to 100, max 1000.
    
</dd>
</dl>

<dl>
<dd>

**query:** `*string` — A search query string for semantic and keyword matching. If omitted, all feature requests are returned (subject to other filters and limit).
    
</dd>
</dl>

<dl>
<dd>

**requestStatuses:** `[]string` — Filter by one or more request statuses. Each value can be a built-in status (new, in_progress, closed, archived) or a custom status slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.Get(ID) -> *pylon.GetFeatureRequestResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single feature request by ID. Optionally includes evidence items when fetch_evidence is true.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsGetRequest{
    ID: "id",
}
client.FeatureRequests.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the feature request to fetch.
    
</dd>
</dl>

<dl>
<dd>

**fetchEvidence:** `*bool` — Whether to include evidence items in the response. Defaults to false.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.Delete(ID) -> *pylon.DeleteFeatureRequestResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a feature request and its associated evidence.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsDeleteRequest{
    ID: "id",
}
client.FeatureRequests.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the feature request to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.Update(ID, request) -> *pylon.UpdateFeatureRequestResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing feature request. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsUpdateRequest{
    ID: "id",
}
client.FeatureRequests.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the feature request to update.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to set. Only passed-in fields will be modified.
    
</dd>
</dl>

<dl>
<dd>

**requestStatus:** `*string` — The new request status. Can be a built-in status (new, in_progress, closed, archived) or a custom status slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.AddEvidence(FeatureRequestID, request) -> *pylon.CreateFeatureRequestEvidenceResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a manual evidence record linking a customer account to a feature request. Repeated requests create separate evidence records.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsAddEvidenceRequest{
    FeatureRequestID: "id",
    AccountID: "account_id",
}
client.FeatureRequests.AddEvidence(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**featureRequestID:** `string` — The ID of the feature request.
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `string` — The ID of the customer account to link to the feature request.
    
</dd>
</dl>

<dl>
<dd>

**summary:** `*string` — A summary explaining why this account is linked. Defaults to "Account manually linked via API."
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.LinkExternalIssue(FeatureRequestID, request) -> *pylon.LinkFeatureRequestExternalIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

By default, links the external issue and creates a backlink to the feature request in the source system. To unlink it, set the operation field to "unlink". Repeating the same link request is a successful no-op.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsLinkExternalIssueRequest{
    FeatureRequestID: "id",
    ExternalIssueID: "external_issue_id",
    Source: "source",
}
client.FeatureRequests.LinkExternalIssue(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**featureRequestID:** `string` — The ID of the feature request to link an external issue to.
    
</dd>
</dl>

<dl>
<dd>

**externalIssueID:** `string` — The ID or human-readable key of the external issue in the source system.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "link" to link the issue (default) or "unlink" to unlink it.
    
</dd>
</dl>

<dl>
<dd>

**source:** `string` — The source system of the external issue (e.g., "linear", "asana", "jira", "github", "shortcut").
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.FeatureRequests.SetPortalVisibility(FeatureRequestID, request) -> *pylon.SetFeatureRequestPortalVisibilityResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Toggles portal visibility for a set of accounts on a feature request. Idempotent — adding already-visible accounts or removing already-hidden accounts is a no-op. Note: visibility only takes effect when the Feature Requests tab is enabled in portal settings.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.FeatureRequestsSetPortalVisibilityRequest{
    FeatureRequestID: "id",
    AccountIDs: []string{
        "account_ids",
    },
    Visible: true,
}
client.FeatureRequests.SetPortalVisibility(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**featureRequestID:** `string` — The ID of the feature request.
    
</dd>
</dl>

<dl>
<dd>

**accountIDs:** `[]string` — The account IDs to add or remove portal visibility for.
    
</dd>
</dl>

<dl>
<dd>

**visible:** `bool` — Whether the specified accounts should be able to see this feature request in the portal. True to add visibility, false to remove.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## IssueGroups
<details><summary><code>client.IssueGroups.Create(request) -> *pylon.CreateIssueGroupResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an issue group and attaches its initial child issues atomically.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssueGroupsCreateRequest{
    ChildIssueIDs: []string{
        "child_issue_ids",
    },
    Title: "title",
}
client.IssueGroups.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**childIssueIDs:** `[]string` — The IDs of the issues to include in the group. At least one is required.
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — The title of the issue group.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## IssueStatuses
<details><summary><code>client.IssueStatuses.List() -> *pylon.GetIssueStatusesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all issue statuses for the organization. Use `slug` as `state` in PATCH /issues and issue search filters.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.IssueStatuses.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues
<details><summary><code>client.Issues.List() -> *pylon.GetIssuesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of issues created within a required time range (max 365 days). Results are sorted by created_at, newest first. To filter on updated_at or other timestamps, use POST /issues/search.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesListRequest{
    StartTime: pylon.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
    EndTime: pylon.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
}
client.Issues.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**startTime:** `time.Time` — The start of the time range, filtering on the issue's created_at (inclusive). Use RFC3339 with Z or a URL-encoded offset (%2B). The duration between start_time and end_time must be less than or equal to 365 days.
    
</dd>
</dl>

<dl>
<dd>

**endTime:** `time.Time` — The end of the time range, filtering on the issue's created_at (exclusive). Use RFC3339 with Z or a URL-encoded offset (%2B). The duration between start_time and end_time must be less than or equal to 365 days.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of issues to fetch. Defaults to 20000. Set to 0 or omit to use the default. Must be between 0 and 20000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Create(request) -> *pylon.CreateIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new issue and its first message. Requires either an account_id or requester information.

Requester fields identify the customer, user_id or contact_id identifies the first-message author, and destination_metadata controls delivery. These choices are independent. If destination_metadata is omitted, the first message is an internal note and no customer is contacted. See the request-field descriptions and examples for destination-specific requirements.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesCreateRequest{
    BodyHTML: "<p>I cannot access my account.</p>",
    ContactID: pylon.String(
        "contact_123",
    ),
    DestinationMetadata: &pylon.DestinationMetadata{
        Destination: pylon.DestinationMetadataDestinationInAppChat,
    },
    RequesterID: pylon.String(
        "contact_123",
    ),
    Title: "Unable to sign in",
}
client.Issues.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `*string` — The account that this issue belongs to. If requester_id is also provided, the requester must belong to this account. If requester_email is provided, the contact is found or created in this account.
    
</dd>
</dl>

<dl>
<dd>

**assigneeID:** `*string` — The user the issue should be assigned to.
    
</dd>
</dl>

<dl>
<dd>

**attachmentURLs:** `[]string` — URLs of files to attach to the issue's first message.
    
</dd>
</dl>

<dl>
<dd>

**authorUnverified:** `*bool` — Whether the requester's identity has NOT been verified. Defaults to false (verified).
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The HTML content of the body of the issue.
    
</dd>
</dl>

<dl>
<dd>

**contactID:** `*string` — The contact to attribute the first message to. This controls the message author, not the issue requester. Makes the message appear as a customer message rather than an internal note. Only one of user_id or contact_id can be provided. Requires destination_metadata.
    
</dd>
</dl>

<dl>
<dd>

**createdAt:** `*time.Time` — Timestamp of when the issue was created. If not specified, the current time will be used. (RFC3339)
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this issue.
    
</dd>
</dl>

<dl>
<dd>

**customIssueSourceID:** `*string` — The ID of a custom issue source (created in the App Directory under Chat > Add Custom Chat App). Sets the issue source to the custom source's slug. Use this for channels Pylon doesn't natively support (e.g. WeChat). Cannot be combined with destination_metadata.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Whether the issue should be visible in the customer portal. When destination is "customer_portal", this is set to true and cannot be false.
    
</dd>
</dl>

<dl>
<dd>

**destinationMetadata:** `*pylon.DestinationMetadata` 
    
</dd>
</dl>

<dl>
<dd>

**priority:** `*pylon.CreateIssueRequestPriority` — The priority of the issue. Can be one of: urgent, high, medium, or low.
    
</dd>
</dl>

<dl>
<dd>

**requesterAvatarURL:** `*string` — The URL of an avatar of the requester.
    
</dd>
</dl>

<dl>
<dd>

**requesterEmail:** `*string` — The email of the customer this issue is for. Used when requester_id is omitted. If no matching contact exists, one will be created. When account_id is provided, the contact is found or created in that account. This does not control who authored the first message.
    
</dd>
</dl>

<dl>
<dd>

**requesterID:** `*string` — The customer this issue is for. Sets the "Requester" shown in the issue sidebar but does not control who authored the first message. If account_id is omitted, the requester's primary account is used when available. If requester_email is also provided, requester_id takes precedence.
    
</dd>
</dl>

<dl>
<dd>

**requesterName:** `*string` — The optional full name of the requester. Used when creating a new contact via requester_email.
    
</dd>
</dl>

<dl>
<dd>

**requesterPhoneNumber:** `*string` — The phone number of a new requester. Only supported for direct WhatsApp delivery and cannot be combined with requester_id, requester_email, requester_name, or requester_avatar_url. The number is normalized to E.164 format and used to create a phone-only contact in the same transaction as the issue.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — An array of strings to use as tags on this issue. If provided, the issue tags will be updated to the given tags.
    
</dd>
</dl>

<dl>
<dd>

**teamID:** `*string` — The ID of the team this issue should be assigned to.
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — The title of the issue.
    
</dd>
</dl>

<dl>
<dd>

**userID:** `*string` — The internal Pylon user to attribute the first message to. This does not assign the user as the requester. Only one of user_id or contact_id can be provided. If neither is set, the API token's user is used.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.BulkUpdate(request) -> *pylon.UpdateIssuesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies the same changes to up to 100 issues. Only provided fields are modified. Issues that do not exist, or that the caller cannot update, are skipped and listed in skipped_issues instead of failing the request.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesBulkUpdateRequest{
    IssueIDs: []string{
        "issue_ids",
    },
}
client.Issues.BulkUpdate(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**assigneeID:** `*string` — The ID of the user to assign the issues to. If empty string is passed in, the issues will be unassigned.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — Custom fields to set on the issues. Only passed in fields are modified. Clearing a custom field is not supported in bulk; use PATCH /issues/{id}.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Whether the issues should be visible in the customer portal.
    
</dd>
</dl>

<dl>
<dd>

**issueIDs:** `[]string` — The IDs of the issues to update. Must contain between 1 and 100 IDs.
    
</dd>
</dl>

<dl>
<dd>

**state:** `*string` — The state to move the issues to. Standard values are `new`, `waiting_on_you`, `waiting_on_customer`, `on_hold`, and `closed`; custom status slugs are also supported.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — Tags to apply to the issues, according to tags_apply_mode.
    
</dd>
</dl>

<dl>
<dd>

**tagsApplyMode:** `*pylon.UpdateIssuesRequestTagsApplyMode` — The mode for applying tags. Valid values: "append_only", "remove_only", "replace". Defaults to "replace".
    
</dd>
</dl>

<dl>
<dd>

**teamID:** `*string` — The ID of the team to assign the issues to. If empty string is passed in, the team will be removed. Team assignment is applied asynchronously.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.MarkSpam(request) -> *pylon.MarkIssuesAsSpamResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Marks up to 100 email issues as spam. Each issue is deleted, and the sender's email address is blocked unless it belongs to your own domains or support inboxes. If an issue's account has no issues left afterwards, the account is deleted too. Issues from other sources are skipped with reason unsupported_source. Issues that do not exist, or that the caller cannot mark as spam, are skipped and listed in skipped_issues instead of failing the request.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesMarkSpamRequest{
    IssueIDs: []string{
        "issue_ids",
    },
}
client.Issues.MarkSpam(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueIDs:** `[]string` — The IDs of the issues to mark as spam. Must contain between 1 and 100 IDs.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Merge(request) -> *pylon.MergeIssuesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Merges one or more issues into a primary issue. All issues must belong to the same account (or, without an account, the same requester). All issues are found and validated before anything changes, so a request rejected for a missing or ineligible issue merges nothing. Closing messages are sent before the merge and are not recalled: if sending one fails, or the merge fails afterwards, duplicates processed earlier may already have received it. This cannot be undone.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesMergeRequest{
    DuplicateIssueIDs: []string{
        "duplicate_issue_ids",
    },
    PrimaryIssueID: "primary_issue_id",
}
client.Issues.Merge(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**closingMessage:** `*string` — Optional plain-text message sent to the customer on each merged Slack or form issue before it is merged.
    
</dd>
</dl>

<dl>
<dd>

**duplicateIssueIDs:** `[]string` — The IDs or numbers of the issues to merge into the primary issue. Must contain between 1 and 50 issues, all in the same account as the primary issue.
    
</dd>
</dl>

<dl>
<dd>

**primaryIssueID:** `string` — The ID or number of the issue to merge into. It keeps its ID and receives the messages of the merged issues.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Search(request) -> *pylon.SearchIssuesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |
 `account_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `customer_portal_visible` | `equals`, `in`, `not_in` |
 `ticket_form_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `requester_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `follower_user_id` | `equals`, `in`, `not_in` |
 `follower_contact_id` | `equals`, `in`, `not_in` |
 `state` | `equals`, `in`, `not_in` |
 `tags` | `contains`, `does_not_contain`, `in`, `not_in` |
 `title` | `string_contains`, `string_does_not_contain` |
 `body_html` | `string_contains`, `string_does_not_contain` |
 `assignee_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `team_id` | `equals`, `in`, `not_in` |
 `issue_type` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `issue_is_issue_group` | `equals`, `in`, `not_in` |
 `resolved_at` | `time_is_after`, `time_is_before`, `time_range` |
 `latest_message_activity_at` | `time_is_after`, `time_is_before`, `time_range` |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |
 `slack_channel_id` | `equals`, `in`, `not_in` |
 `workspace_email` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `reopened` | `equals`, `in`, `not_in` |

Timestamp values use RFC3339 format. Standard `state` values are `new`, `waiting_on_you`, `waiting_on_customer`, `on_hold`, and `closed`; custom status slugs are also supported. `issue_type` values are `conversation` and `ticket`.

For tag filters, pass the tag name. For custom fields, pass the field slug as `field`. `slack_channel_id` identifies the Slack channel where the issue was created. `workspace_email` identifies the email address connected to the Pylon workspace through which the issue's email conversation is routed. `customer_portal_visible` values are `true` and `false`; issue groups are never visible in the customer portal, so they always match `false`. `reopened` values are `true` and `false`; it is a sticky flag set the first time an issue is reopened after being resolved, and it records no timestamp.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesSearchRequest{
    Filter: &pylon.Filter{
        Field: pylon.String(
            "state",
        ),
        Operator: pylon.FilterOperatorEquals,
        Value: pylon.String(
            "new",
        ),
    },
}
client.Issues.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of issues to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>

<dl>
<dd>

**searchText:** `*string` — Fuzzy text search. Results are intersected with any provided filter.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Get(ID) -> *pylon.GetIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single issue by ID or issue number.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesGetRequest{
    ID: "id",
}
client.Issues.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID or number of the issue to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Delete(ID) -> *pylon.DeleteIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes an issue by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesDeleteRequest{
    ID: "id",
}
client.Issues.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the issue to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Update(ID, request) -> *pylon.UpdateIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing issue. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesUpdateRequest{
    ID: "id",
}
client.Issues.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the issue to update.
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `*string` — The ID of the account that this issue belongs to. To remove the account, pass an empty string and also provide requester_id. The requester can be cleared with an empty string or retained if it has no account memberships. Account removal is supported only for manual, form, and email issues.
    
</dd>
</dl>

<dl>
<dd>

**assigneeID:** `*string` — The ID of the user who should be assigned to this issue. If empty string is passed in, the issue assignee will be removed.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this issue. Only passed in fields will be modified.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Whether the issue should be visible in the customer portal.
    
</dd>
</dl>

<dl>
<dd>

**requesterID:** `*string` — The ID of the requester that this issue is on behalf of. If an empty string is passed, the requester will be removed. This field must be provided when removing the issue's account, and a retained requester must not belong to any account.
    
</dd>
</dl>

<dl>
<dd>

**requestorID:** `*string` — Deprecated: Use requester_id instead.
    
</dd>
</dl>

<dl>
<dd>

**state:** `*string` — The state this issue should be moved to. Standard values are `new`, `waiting_on_you`, `waiting_on_customer`, `on_hold`, and `closed`; custom status slugs are also supported.
    
</dd>
</dl>

<dl>
<dd>

**tags:** `[]string` — An array of strings to use as tags on this issue. If provided, the issue tags will be updated to be exactly the given tags.
    
</dd>
</dl>

<dl>
<dd>

**teamID:** `*string` — The ID of the team this issue should be assigned to. If empty string is passed in, any assigned team will be removed.
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — The title of the issue.
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*pylon.UpdateIssueRequestBodyType` — The type of the issue. Set to "ticket" to upgrade a conversation to a support ticket. Cannot be downgraded from "ticket" to "conversation".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.CreateAiResponse(IssueID, request) -> *pylon.CreateIssueAiResponseResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generates an AI response for the specified issue using the given agent.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesCreateAiResponseRequest{
    IssueID: "id",
    AiAgentID: "ai_agent_id",
}
client.Issues.CreateAiResponse(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to create an AI response for.
    
</dd>
</dl>

<dl>
<dd>

**aiAgentID:** `string` — The ID of the AI agent to use to create the AI response.
    
</dd>
</dl>

<dl>
<dd>

**postAsInternalNote:** `*bool` — Whether to post the AI response as an internal note on the issue.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.CreateDraftReply(IssueID, request) -> *pylon.CreateIssueDraftReplyResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a private customer-reply draft without sending it. The draft is visible only to its owner and may require a normal issue refetch before appearing in the app. For unlinked or service API tokens, user_id is required. This endpoint updates only untouched drafts that it previously created; every other existing draft returns a conflict.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesCreateDraftReplyRequest{
    IssueID: "id",
    BodyHTML: "body_html",
}
client.Issues.CreateDraftReply(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue.
    
</dd>
</dl>

<dl>
<dd>

**bccEmails:** `[]string` — The draft's BCC recipients. See to_emails.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The draft body in HTML.
    
</dd>
</dl>

<dl>
<dd>

**ccEmails:** `[]string` — The draft's CC recipients. See to_emails.
    
</dd>
</dl>

<dl>
<dd>

**toEmails:** `[]string` — The draft's To recipients. If any of to_emails, cc_emails, or bcc_emails is provided, the draft uses exactly those lists and an omitted list is saved empty; omit all three to use the composer's default recipients.
    
</dd>
</dl>

<dl>
<dd>

**userID:** `*string` — The active Pylon user who should own and see the draft. Defaults to the API-token user when it is a human Pylon user; required for unlinked or service API tokens.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.LinkExternalIncident(IssueID, request) -> *pylon.LinkExternalIncidentResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Links an incident from one of the organization's connected incident systems (incident.io or Rootly). An issue can have several linked incidents, and linking one that is already linked has no effect. To unlink, set the operation field to "unlink".

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesLinkExternalIncidentRequest{
    IssueID: "id",
    IncidentID: "incident_id",
    Source: pylon.LinkExternalIncidentRequestBodySourceIncidentIo,
}
client.Issues.LinkExternalIncident(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to link the incident to.
    
</dd>
</dl>

<dl>
<dd>

**incidentID:** `string` — The incident's reference (such as INC-123 or ROOT-123) or its ID in the incident system.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "link" to link the incident (default) or "unlink" to unlink it.
    
</dd>
</dl>

<dl>
<dd>

**source:** `pylon.LinkExternalIncidentRequestBodySource` 

The incident system the incident belongs to. It must be connected to the organization.
Valid values: "incident_io", "rootly"
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.LinkExternalIssue(IssueID, request) -> *pylon.LinkExternalIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

By default, links external issues. To unlink issues, set the operation field to "unlink".

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesLinkExternalIssueRequest{
    IssueID: "id",
    ExternalIssueID: "external_issue_id",
    Source: "source",
}
client.Issues.LinkExternalIssue(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to link external issues to.
    
</dd>
</dl>

<dl>
<dd>

**externalIssueID:** `string` — The ID of the external issue in the source system.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "link" to link issues (default) or "unlink" to unlink issues.
    
</dd>
</dl>

<dl>
<dd>

**source:** `string` — The source system of the external issue (e.g., "linear", "asana", "jira", "github", "shortcut").
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.CreateNote(IssueID, request) -> *pylon.CreateIssueNoteResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Posts an internal note on an issue thread. Not visible to the requester.

Thread selection:
* If thread_id is provided, posts to that internal thread.
* If message_id is provided, posts to the thread containing that internal note.
* Providing both thread_id and message_id returns a 400 response.
* If neither is provided, posts to the most recently created Slack-backed internal thread. If none exists, creates a Pylon-only internal thread.
* thread_name names that newly created Pylon-only thread and is otherwise ignored.

Empty thread_id, message_id, and thread_name values are treated as omitted.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesCreateNoteRequest{
    IssueID: "id",
    BodyHTML: "body_html",
}
client.Issues.CreateNote(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue.
    
</dd>
</dl>

<dl>
<dd>

**attachmentURLs:** `[]string` — URLs of files to attach to this internal note.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The body of the message in HTML.
    
</dd>
</dl>

<dl>
<dd>

**messageID:** `*string` — The ID of an internal note whose thread should receive the new note. Use the top-level `id` from GET /issues/{id}/messages. Cannot be combined with thread_id.
    
</dd>
</dl>

<dl>
<dd>

**threadID:** `*string` — The ID of the internal thread to post the note to. Use the `id` field (not `thread_id`) from GET /issues/{id}/threads. Cannot be combined with message_id.
    
</dd>
</dl>

<dl>
<dd>

**threadName:** `*string` — Optional name for a new Pylon-only internal thread. Used only when neither thread_id nor message_id is provided and no Slack-backed internal thread exists.
    
</dd>
</dl>

<dl>
<dd>

**userID:** `*string` — Optional user ID to post the message as. If not provided, the API token user will be used.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Reply(IssueID, request) -> *pylon.CreateIssueReplyResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a customer-facing reply on an issue, visible to the requester.

message_id is required to identify which existing customer-visible conversation or thread to continue. Use the top-level message id returned by GET /issues/{id}/messages; do not use an external provider's message ID or the nested email_info.message_id value.

For an email conversation, email_info must contain at least one recipient across to_emails, cc_emails, and bcc_emails. The referenced message controls email threading, but its recipients are not copied automatically.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesReplyRequest{
    IssueID: "id",
    BodyHTML: "body_html",
    MessageID: "message_id",
}
client.Issues.Reply(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue.
    
</dd>
</dl>

<dl>
<dd>

**attachmentURLs:** `[]string` — URLs of files to attach to this reply.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The body of the message in HTML.
    
</dd>
</dl>

<dl>
<dd>

**contactID:** `*string` — Optional contact ID to post the message as. Only one of user_id or contact_id can be provided.
    
</dd>
</dl>

<dl>
<dd>

**customSource:** `*pylon.CustomSourceInfo` 
    
</dd>
</dl>

<dl>
<dd>

**emailInfo:** `*pylon.CreateIssueReplyEmailInfo` 
    
</dd>
</dl>

<dl>
<dd>

**messageID:** `string` — The top-level Pylon message ID to reply to, from the `id` field returned by GET /issues/{id}/messages. The message must belong to the issue in the request path and must be customer-visible, not an internal note. This selects the external conversation or thread where the reply is delivered. For email, it also sets the In-Reply-To and References chain. Do not use a provider-specific message ID or email_info.message_id.
    
</dd>
</dl>

<dl>
<dd>

**userID:** `*string` — Optional user ID to post the message as. Only one of user_id or contact_id can be provided.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Snooze(IssueID, request) -> *pylon.SnoozeIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Snoozes an issue until the specified date and time.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.IssuesSnoozeRequest{
    IssueID: "id",
    SnoozeUntil: pylon.MustParseDateTime(
        "2024-01-15T09:30:00Z",
    ),
}
client.Issues.Snooze(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to snooze.
    
</dd>
</dl>

<dl>
<dd>

**snoozeUntil:** `time.Time` — The date and time to snooze the issue until. (RFC3339)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## KnowledgeBases
<details><summary><code>client.KnowledgeBases.List() -> *pylon.GetKnowledgeBasesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all knowledge bases for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.KnowledgeBases.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Get(ID) -> *pylon.GetKnowledgeBaseResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single knowledge base by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.KnowledgeBasesGetRequest{
    ID: "id",
}
client.KnowledgeBases.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the knowledge base.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## MacroGroups
<details><summary><code>client.MacroGroups.List() -> *pylon.GetMacroGroupsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all macro groups for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.MacroGroups.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Macros
<details><summary><code>client.Macros.List() -> *pylon.GetMacrosResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all macros for the organization. Optionally filter by macro group ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MacrosListRequest{}
client.Macros.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**macroGroupID:** `*string` — Filter macros by macro group ID.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Macros.Create(request) -> *pylon.CreateMacroResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new macro within the specified macro group.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MacrosCreateRequest{
    MacroGroupID: "macro_group_id",
    Name: "name",
    TextHTML: "text_html",
}
client.Macros.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**conditions:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**editVisibility:** `*pylon.VisibilityInput` 
    
</dd>
</dl>

<dl>
<dd>

**macroGroupID:** `string` — The ID of the macro group this macro belongs to.
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — The name of the macro.
    
</dd>
</dl>

<dl>
<dd>

**textHTML:** `string` — The HTML content of the macro.
    
</dd>
</dl>

<dl>
<dd>

**textType:** `*string` — The type of text: "reply", "note", or "email". Defaults to "reply".
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `*pylon.VisibilityInput` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Macros.Get(ID) -> *pylon.GetMacroResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single macro by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MacrosGetRequest{
    ID: "id",
}
client.Macros.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the macro.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Macros.Delete(ID) -> *pylon.DeleteMacroResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a macro by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MacrosDeleteRequest{
    ID: "id",
}
client.Macros.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the macro to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Macros.Update(ID, request) -> *pylon.UpdateMacroResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing macro by ID. All fields are optional; only provided fields will be updated.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MacrosUpdateRequest{
    ID: "id",
}
client.Macros.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the macro to update.
    
</dd>
</dl>

<dl>
<dd>

**conditions:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**editVisibility:** `*pylon.VisibilityInput` 
    
</dd>
</dl>

<dl>
<dd>

**macroGroupID:** `*string` — The ID of the macro group this macro belongs to.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the macro.
    
</dd>
</dl>

<dl>
<dd>

**textHTML:** `*string` — The HTML content of the macro.
    
</dd>
</dl>

<dl>
<dd>

**textType:** `*string` — The type of text: "reply", "note", or "email".
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `*pylon.VisibilityInput` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Me
<details><summary><code>client.Me.Get() -> *pylon.GetMeResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the organization and user associated with the credentials used for authentication.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Me.Get(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Milestones
<details><summary><code>client.Milestones.Create(request) -> *pylon.CreateMilestoneResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new milestone within a project.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MilestonesCreateRequest{
    Name: "name",
    ProjectID: "project_id",
}
client.Milestones.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `*string` — Account ID for this project
    
</dd>
</dl>

<dl>
<dd>

**dueDate:** `*time.Time` — Due date for this milestone, in RFC 3339 format
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — Name for this milestone
    
</dd>
</dl>

<dl>
<dd>

**projectID:** `string` — Project ID for this milestone
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Milestones.Search(request) -> *pylon.SearchMilestonesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `project_id` | `equals`, `in`, `not_in` |
 `account_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `due_date` | `time_is_after`, `time_is_before`, `time_range`, `is_set`, `is_unset` |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |
 `started_at` | `time_is_after`, `time_is_before`, `time_range`, `is_set` |
 `completed_at` | `time_is_after`, `time_is_before`, `time_range`, `is_set` |

Timestamp values use RFC3339 format. Milestones belonging to an unlaunched project are not returned.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MilestonesSearchRequest{}
client.Milestones.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of milestones to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Milestones.Get(ID) -> *pylon.GetMilestoneResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single milestone by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MilestonesGetRequest{
    ID: "id",
}
client.Milestones.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the milestone to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Milestones.Delete(ID) -> *pylon.DeleteMilestoneResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a milestone by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MilestonesDeleteRequest{
    ID: "id",
}
client.Milestones.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the milestone to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Milestones.Update(ID, request) -> *pylon.UpdateMilestoneResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing milestone. Only provided fields are modified.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.MilestonesUpdateRequest{
    ID: "id",
}
client.Milestones.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the milestone to update.
    
</dd>
</dl>

<dl>
<dd>

**dueDate:** `*string` — Due date for this milestone, in RFC 3339 format. Set to an empty string to clear it.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Name for this milestone
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Projects
<details><summary><code>client.Projects.Create(request) -> *pylon.CreateProjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new project for an account. Provide a name or project_template_id. A template supplies defaults; non-empty name and description_html values and supplied customer_portal_visible and owner_id values override them. Supplying either start_date or end_date replaces both template dates.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ProjectsCreateRequest{
    AccountID: "account_id",
}
client.Projects.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — Account ID for this project
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Customer portal visible for this project
    
</dd>
</dl>

<dl>
<dd>

**descriptionHTML:** `*string` — Description HTML for this project
    
</dd>
</dl>

<dl>
<dd>

**endDate:** `*time.Time` — End date for this project, in RFC 3339 format
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Name for this project. Required unless project_template_id is provided. When both are provided, this name overrides the template's name.
    
</dd>
</dl>

<dl>
<dd>

**ownerID:** `*string` — Owner ID for this project
    
</dd>
</dl>

<dl>
<dd>

**projectTemplateID:** `*string` — Project template ID for this project. When provided, it supplies defaults; non-empty name and description_html values and supplied customer_portal_visible and owner_id values override them. Supplying either start_date or end_date replaces both template dates.
    
</dd>
</dl>

<dl>
<dd>

**startDate:** `*time.Time` — Start date for this project, in RFC 3339 format
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Projects.Search(request) -> *pylon.SearchProjectsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `account_id` | `equals`, `in`, `not_in`, `is_set` |
 `status` | `equals`, `in`, `not_in` |
 `owner_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `is_archived` | `equals` |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |

Timestamp values use RFC3339 format. Valid `status` values are `not_started`, `in_progress`, and `completed`. For custom fields, pass the field slug as `field`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ProjectsSearchRequest{}
client.Projects.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of projects to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Projects.Get(ID) -> *pylon.GetProjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single project by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ProjectsGetRequest{
    ID: "id",
}
client.Projects.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the project to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Projects.Delete(ID) -> *pylon.DeleteProjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a project by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ProjectsDeleteRequest{
    ID: "id",
}
client.Projects.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the project to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Projects.Update(ID, request) -> *pylon.UpdateProjectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing project. Only provided fields are modified.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.ProjectsUpdateRequest{
    ID: "id",
}
client.Projects.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the project to update.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this project. Only passed in fields will be modified.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Customer portal visible for this project
    
</dd>
</dl>

<dl>
<dd>

**descriptionHTML:** `*string` — Description HTML for this project
    
</dd>
</dl>

<dl>
<dd>

**endDate:** `*string` — End date for this project, in RFC 3339 format. Set to an empty string to clear it.
    
</dd>
</dl>

<dl>
<dd>

**isArchived:** `*bool` — Whether the project is archived
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — Name for this project
    
</dd>
</dl>

<dl>
<dd>

**ownerID:** `*string` — Owner ID for this project
    
</dd>
</dl>

<dl>
<dd>

**startDate:** `*string` — Start date for this project, in RFC 3339 format. Set to an empty string to clear it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Surveys
<details><summary><code>client.Surveys.List() -> *pylon.GetSurveysResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all surveys for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Surveys.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Surveys.Search(request) -> *pylon.SearchSurveysResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |

Timestamp values use RFC3339 format.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.SurveysSearchRequest{}
client.Surveys.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of surveys to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Surveys.Get(ID) -> *pylon.GetSurveyResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single survey by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.SurveysGetRequest{
    ID: "id",
}
client.Surveys.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the survey.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tags
<details><summary><code>client.Tags.List() -> *pylon.GetTagsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all tags for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Tags.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Create(request) -> *pylon.CreateTagResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new tag with the specified value and object type.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TagsCreateRequest{
    ObjectType: pylon.CreateTagRequestBodyObjectTypeAccount,
    Value: "value",
}
client.Tags.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**hexColor:** `*string` — The hex code of the tag's color.
    
</dd>
</dl>

<dl>
<dd>

**objectType:** `pylon.CreateTagRequestBodyObjectType` — The object type of the associated object. Can be "account", "article", or "issue".
    
</dd>
</dl>

<dl>
<dd>

**value:** `string` — The tag value.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Search(request) -> *pylon.SearchTagsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns tags the caller can read, newest first, optionally narrowed to one object type and to values containing search_text.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TagsSearchRequest{}
client.Tags.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of tags to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>

<dl>
<dd>

**objectType:** `*pylon.SearchTagsRequestObjectType` — Only return tags of this object type. Omit to search every type the caller can read.
    
</dd>
</dl>

<dl>
<dd>

**searchText:** `*string` — Only return tags whose value contains this text. Spaces, hyphens, and underscores match each other.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Get(ID) -> *pylon.GetTagResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single tag by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TagsGetRequest{
    ID: "id",
}
client.Tags.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the tag.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Delete(ID) -> *pylon.DeleteTagResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a tag by ID.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TagsDeleteRequest{
    ID: "id",
}
client.Tags.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the tag to update.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Update(ID, request) -> *pylon.UpdateTagResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing tag. Only provided fields are modified.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TagsUpdateRequest{
    ID: "id",
}
client.Tags.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the tag to update.
    
</dd>
</dl>

<dl>
<dd>

**hexColor:** `*string` — The hex code of the tag's color.
    
</dd>
</dl>

<dl>
<dd>

**value:** `*string` 

in: body
The name of the tag.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TaskStatuses
<details><summary><code>client.TaskStatuses.List() -> *pylon.GetTaskStatusesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all task statuses for the organization.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.TaskStatuses.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tasks
<details><summary><code>client.Tasks.List() -> *pylon.GetTasksResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of tasks for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksListRequest{}
client.Tasks.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of tasks to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Create(request) -> *pylon.CreateTaskResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new task with a title and optional metadata.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksCreateRequest{
    Title: "title",
}
client.Tasks.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `*string` — Account ID for this task
    
</dd>
</dl>

<dl>
<dd>

**assigneeID:** `*string` — Assignee ID for this task
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — Body HTML for this task
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this task.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Customer portal visible for this task
    
</dd>
</dl>

<dl>
<dd>

**dueDate:** `*time.Time` — Due date for this task, in RFC 3339 format
    
</dd>
</dl>

<dl>
<dd>

**milestoneID:** `*string` — Milestone ID for this task
    
</dd>
</dl>

<dl>
<dd>

**parentTaskID:** `*string` — Parent task ID, to create this task as a subtask
    
</dd>
</dl>

<dl>
<dd>

**projectID:** `*string` — Project ID for this task
    
</dd>
</dl>

<dl>
<dd>

**status:** `*pylon.TaskStatus` 
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — Title for this task
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Search(request) -> *pylon.SearchTasksResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `account_id` | `equals`, `in`, `not_in`, `is_set` |
 `project_id` | `equals`, `in`, `not_in`, `is_set`, `is_unset` |
 `status` | `equals`, `in`, `not_in` |
 `assignee_id` | `equals`, `in`, `not_in`, `is_set` |
 `milestone_id` | `equals`, `in`, `not_in`, `is_set` |
 `created_at` | `time_is_after`, `time_is_before`, `time_range` |
 `due_date` | `time_is_after`, `time_is_before`, `time_range`, `is_set` |
 `updated_at` | `time_is_after`, `time_is_before`, `time_range` |

Timestamp values use RFC3339 format. Valid `status` values are `not_started`, `in_progress`, and `completed`. For custom fields, pass the field slug as `field`.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksSearchRequest{}
client.Tasks.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of tasks to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Get(ID) -> *pylon.GetTaskResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single task by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksGetRequest{
    ID: "id",
}
client.Tasks.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the task to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Delete(ID) -> *pylon.DeleteTaskResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a task by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksDeleteRequest{
    ID: "id",
}
client.Tasks.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the task to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Update(ID, request) -> *pylon.UpdateTaskResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing task. Only provided fields are modified.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksUpdateRequest{
    ID: "id",
}
client.Tasks.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the task to update.
    
</dd>
</dl>

<dl>
<dd>

**assigneeID:** `*string` — Assignee ID for this task
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — Body HTML for this task
    
</dd>
</dl>

<dl>
<dd>

**completedAt:** `*time.Time` — Completed at time for this task, in RFC 3339 format. The task must already have a completed status and completion date.
    
</dd>
</dl>

<dl>
<dd>

**customFields:** `[]*pylon.CustomFieldValue` — An array of custom fields to be used on this task. Only passed in fields will be modified.
    
</dd>
</dl>

<dl>
<dd>

**customerPortalVisible:** `*bool` — Customer portal visible for this task
    
</dd>
</dl>

<dl>
<dd>

**dueDate:** `*string` — Due date for this task, in RFC 3339 format. Set to an empty string to clear it.
    
</dd>
</dl>

<dl>
<dd>

**milestoneID:** `*string` — Milestone ID for this task
    
</dd>
</dl>

<dl>
<dd>

**projectID:** `*string` — Project ID for this task
    
</dd>
</dl>

<dl>
<dd>

**status:** `*pylon.TaskStatus` 
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — Title for this task
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.LinkExternalIssue(TaskID, request) -> *pylon.LinkTaskExternalIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

By default, links the external issue. To unlink it, set the operation field to "unlink". Repeating the same link request is a successful no-op.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksLinkExternalIssueRequest{
    TaskID: "id",
    ExternalIssueID: "external_issue_id",
    Source: "source",
}
client.Tasks.LinkExternalIssue(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task to link an external issue to.
    
</dd>
</dl>

<dl>
<dd>

**externalIssueID:** `string` — The ID or human-readable key of the external issue in the source system.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "link" to link the issue (default) or "unlink" to unlink it.
    
</dd>
</dl>

<dl>
<dd>

**source:** `string` — The source system of the external issue (e.g., "linear", "asana", "jira", "github", "shortcut").
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.LinkIssue(TaskID, request) -> *pylon.LinkTaskIssueResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Links the issue to the task by default. To unlink it, set the operation field to "unlink".

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TasksLinkIssueRequest{
    TaskID: "id",
    IssueID: "issue_id",
}
client.Tasks.LinkIssue(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task to link a Pylon issue to.
    
</dd>
</dl>

<dl>
<dd>

**issueID:** `string` — The ID of the Pylon issue.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "link" to link the issue (default) or "unlink" to unlink it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Teams
<details><summary><code>client.Teams.List() -> *pylon.GetTeamsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all teams for the organization, each with how it assigns issues and its recurring
assignment schedule if it has one.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Teams.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Teams.Create(request) -> *pylon.CreateTeamResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new team with a name and optional member list. Optionally sets how the team
assigns issues and creates its recurring assignment schedule in the same call.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TeamsCreateRequest{
    Name: "name",
}
client.Teams.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**assignmentConfiguration:** `*pylon.TeamAssignmentConfigurationInput` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `string` — The name of the team.
    
</dd>
</dl>

<dl>
<dd>

**schedule:** `*pylon.TeamScheduleInput` 
    
</dd>
</dl>

<dl>
<dd>

**userIDs:** `[]string` — The list of user IDs to add to the team.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Teams.Get(ID) -> *pylon.GetTeamResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single team by ID, with how it assigns issues and its recurring assignment
schedule if it has one.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TeamsGetRequest{
    ID: "id",
}
client.Teams.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the team to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Teams.Update(ID, request) -> *pylon.UpdateTeamResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing team, including how it assigns issues and its recurring assignment
schedule. Only provided fields are modified; supplying schedule.blocks replaces the whole
rotation, and omitting it leaves the rotation unchanged.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TeamsUpdateRequest{
    ID: "id",
}
client.Teams.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the team to update.
    
</dd>
</dl>

<dl>
<dd>

**assignmentConfiguration:** `*pylon.TeamAssignmentConfigurationInput` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the team.
    
</dd>
</dl>

<dl>
<dd>

**schedule:** `*pylon.TeamScheduleInput` 
    
</dd>
</dl>

<dl>
<dd>

**userIDs:** `[]string` — The list of user IDs to add to the team. If provided, the team members will be updated to be exactly the given users.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TicketForms
<details><summary><code>client.TicketForms.List() -> *pylon.GetTicketFormsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all ticket forms for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.TicketForms.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TicketForms.Get(ID) -> *pylon.GetTicketFormResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single ticket form by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TicketFormsGetRequest{
    ID: "id",
}
client.TicketForms.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the ticket form to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TicketForms.Submit(TicketFormID, request) -> *pylon.SubmitTicketFormResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an issue from a configured ticket form. Provide either requester_id or both requester_email and requester_name. Field types are inferred from the ticket form; use value for single-value fields and values for multi-value and file-upload fields.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TicketFormsSubmitRequest{
    TicketFormID: "id",
}
client.TicketForms.Submit(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ticketFormID:** `string` — The ID of the ticket form to submit.
    
</dd>
</dl>

<dl>
<dd>

**attachmentURLs:** `[]string` — HTTPS URLs to attach to the initial ticket message. URLs are copied into durable Pylon storage before the submission is persisted.
    
</dd>
</dl>

<dl>
<dd>

**fields:** `[]*pylon.SubmitTicketFormField` — The submitted ticket form fields. Use the slugs returned by GET /ticket-forms/{id}, excluding name and email, which are supplied through the requester fields above.
    
</dd>
</dl>

<dl>
<dd>

**requesterEmail:** `*string` — The requester's email address. Must be provided with requester_name and cannot be combined with requester_id.
    
</dd>
</dl>

<dl>
<dd>

**requesterID:** `*string` — The ID of an existing contact to use as the requester. Provide either requester_id or both requester_email and requester_name.
    
</dd>
</dl>

<dl>
<dd>

**requesterName:** `*string` — The requester's full name. Must be provided with requester_email and cannot be combined with requester_id.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TrainingData
<details><summary><code>client.TrainingData.List() -> *pylon.ListTrainingDataResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all training data configurations for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.TrainingData.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TrainingData.Create(request) -> *pylon.CreateTrainingDataResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new training data configuration for the organization.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TrainingDataCreateRequest{}
client.TrainingData.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**trainingDataName:** `*string` — The name of the training data container.
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `*pylon.CreateTrainingDataRequestBodyVisibility` 

The visibility of the training data. Defaults to "everyone".
Valid values: "everyone", "user_only", "ai_agent_only"
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TrainingData.UploadFiles(request) -> *pylon.TrainingDataUploadResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads one or more files to a training data configuration.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TrainingDataUploadFilesRequest{
    Files: []string{
        "files",
    },
}
client.TrainingData.UploadFiles(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TrainingData.UploadContent(request) -> *pylon.TrainingDataUploadResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads plain text content as a training data document.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TrainingDataUploadContentRequest{}
client.TrainingData.UploadContent(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**content:** `*string` — The text content to upload.
    
</dd>
</dl>

<dl>
<dd>

**externalID:** `*string` — External ID for idempotent operations (optional).
    
</dd>
</dl>

<dl>
<dd>

**fileName:** `*string` — The name for the uploaded file.
    
</dd>
</dl>

<dl>
<dd>

**trainingDataID:** `*string` — The ID of an existing training data container to upload to (optional).
    
</dd>
</dl>

<dl>
<dd>

**trainingDataName:** `*string` — The name of a new training data container (required if training_data_id not provided).
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `*pylon.UploadTrainingDataFileContentRequestBodyVisibility` — Visibility of the training data. Defaults to "everyone".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.TrainingData.Get(ID) -> *pylon.GetTrainingDataResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single training data configuration by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.TrainingDataGetRequest{
    ID: "id",
}
client.TrainingData.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the training data.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## UserRoles
<details><summary><code>client.UserRoles.List() -> *pylon.GetUserRolesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all user roles for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.UserRoles.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## UserStatuses
<details><summary><code>client.UserStatuses.List() -> *pylon.GetUserStatusesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the built-in and custom user statuses for the organization. Use `slug` in a team's `assignment_configuration.assignable_user_statuses`.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.UserStatuses.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Users
<details><summary><code>client.Users.List() -> *pylon.GetUsersResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all users for the organization.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.UsersListRequest{}
client.Users.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**includeDeactivated:** `*bool` — Whether to include deactivated users. Defaults to false.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Users.Search(request) -> *pylon.SearchUsersResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Filterable fields and their allowed operators:

 Field | Allowed operators |
 --- | --- |
 `email` | `equals`, `in`, `not_in` |

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.UsersSearchRequest{}
client.Users.Search(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**filter:** `*pylon.Filter` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of users to fetch. Defaults to 100. Must be between 1 and 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Users.Get(ID) -> *pylon.GetUserResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single user by ID.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.UsersGetRequest{
    ID: "id",
}
client.Users.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the user to fetch.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Users.Update(ID, request) -> *pylon.GetUserResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing user. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &pylon.UsersUpdateRequest{
    ID: "id",
}
client.Users.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` — The ID of the user to update.
    
</dd>
</dl>

<dl>
<dd>

**avatarURL:** `*string` — The avatar URL of the user. Must be a square .png, .jpg or .jpeg.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the user.
    
</dd>
</dl>

<dl>
<dd>

**roleID:** `*string` — The role_id of the user.
    
</dd>
</dl>

<dl>
<dd>

**status:** `*string` — The new status for the user: `active`, `away`, `out_of_office`, or a custom status slug from GET /user-statuses.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Accounts Highlights
<details><summary><code>client.Accounts.Highlights.Create(AccountID, request) -> *pylon.CreateAccountHighlightResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new highlight on an account.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsHighlightsCreateRequest{
    AccountID: "account_id",
    ContentHTML: "content_html",
}
client.Accounts.Highlights.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account that the highlight belongs to.
    
</dd>
</dl>

<dl>
<dd>

**contactID:** `*string` — Optional ID or external ID of a contact to associate the resulting memory with. The contact must belong to the account.
    
</dd>
</dl>

<dl>
<dd>

**contentHTML:** `string` — The HTML content for this highlight.
    
</dd>
</dl>

<dl>
<dd>

**expiresAt:** `*time.Time` — Optional RFC3339 timestamp of when this highlight will expire.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Highlights.Delete(AccountID, HighlightID) -> *pylon.DeleteAccountHighlightResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes an account highlight by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsHighlightsDeleteRequest{
    AccountID: "account_id",
    HighlightID: "highlight_id",
}
client.Accounts.Highlights.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account that the highlight belongs to.
    
</dd>
</dl>

<dl>
<dd>

**highlightID:** `string` — The ID of the highlight to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Highlights.Update(AccountID, HighlightID, request) -> *pylon.UpdateAccountHighlightResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing account highlight. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsHighlightsUpdateRequest{
    AccountID: "account_id",
    HighlightID: "highlight_id",
}
client.Accounts.Highlights.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account that the highlight belongs to.
    
</dd>
</dl>

<dl>
<dd>

**highlightID:** `string` — The ID of the highlight to update.
    
</dd>
</dl>

<dl>
<dd>

**contentHTML:** `*string` — The updated HTML content for this highlight.
    
</dd>
</dl>

<dl>
<dd>

**expiresAt:** `*string` — The updated expires at timestamp (RFC3339). Omit it to keep the current expiry, or set it to an empty string to clear it.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Accounts Relationships
<details><summary><code>client.Accounts.Relationships.Create(AccountID, request) -> *pylon.CreateAccountRelationshipResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a parent or partner relationship for the account in the URL.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsRelationshipsCreateRequest{
    AccountID: "account_id",
    RelatedObjectID: "related_object_id",
    RelationshipType: "relationship_type",
}
client.Accounts.Relationships.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID of the child or client account.
    
</dd>
</dl>

<dl>
<dd>

**relatedObjectID:** `string` — The ID of the related parent or partner account.
    
</dd>
</dl>

<dl>
<dd>

**relationshipType:** `string` — The relationship type. Must be "parent_account" or "partner_account".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Relationships.List(AccountID) -> *pylon.GetAccountRelationshipsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the parent-child and partner-client relationships where the account is the child or client.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsRelationshipsListRequest{
    AccountID: "account_id",
}
client.Accounts.Relationships.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID of the child or client account whose relationships should be returned.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Relationships.Delete(AccountID, RelationshipID) -> *pylon.DeleteAccountRelationshipResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes an account relationship by ID.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsRelationshipsDeleteRequest{
    AccountID: "account_id",
    RelationshipID: "relationship_id",
}
client.Accounts.Relationships.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID of the child or client account.
    
</dd>
</dl>

<dl>
<dd>

**relationshipID:** `string` — The ID of the account relationship to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Accounts Activities
<details><summary><code>client.Accounts.Activities.List(AccountID) -> *pylon.GetActivitiesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns custom activities for the specified account, ordered from newest to oldest.
The {id} parameter accepts either:
Internal account ID (UUID format)
External ID (any string format)

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsActivitiesListRequest{
    AccountID: "id",
}
client.Accounts.Activities.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account to fetch activities for.
    
</dd>
</dl>

<dl>
<dd>

**activityType:** `*string` — The custom activity type slug to filter by.
    
</dd>
</dl>

<dl>
<dd>

**startTime:** `*time.Time` — The start time (RFC3339) of the activity time range.
    
</dd>
</dl>

<dl>
<dd>

**endTime:** `*time.Time` — The end time (RFC3339) of the activity time range.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of activities to fetch. Defaults to 100. Must be greater than 0 and less than or equal to 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.Activities.Create(AccountID, request) -> *pylon.CreateActivityResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The {id} parameter accepts either:
Internal account ID (UUID format)
External ID (any string format)

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &accounts.AccountsActivitiesCreateRequest{
    AccountID: "id",
    Slug: "slug",
}
client.Accounts.Activities.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account to create the activity for.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — Optional HTML content to display in the activity.
    
</dd>
</dl>

<dl>
<dd>

**contactID:** `*string` — Optional contact ID of the actor of the activity.
    
</dd>
</dl>

<dl>
<dd>

**happenedAt:** `*time.Time` — Timestamp (RFC3339) of when the activity happened. Defaults to the current time if empty.
    
</dd>
</dl>

<dl>
<dd>

**link:** `*string` — Optional link to add to the activity.
    
</dd>
</dl>

<dl>
<dd>

**linkText:** `*string` — Optional link text to display on the activity. Defaults to "Open link" if not provided. Applies only if a link is provided.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `string` — The slug of the activity to create.
    
</dd>
</dl>

<dl>
<dd>

**userID:** `*string` — Optional user ID of the actor of the activity.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Accounts NotebookBlocks Notes
<details><summary><code>client.Accounts.NotebookBlocks.Notes.List(AccountID, BlockID) -> *pylon.GetAccountNotebookNotesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns notes from a specific Notes block in an account notebook.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &notebookblocks.AccountsNotebookBlocksNotesListRequest{
    AccountID: "account_id",
    BlockID: "block_id",
}
client.Accounts.NotebookBlocks.Notes.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account.
    
</dd>
</dl>

<dl>
<dd>

**blockID:** `string` — The ID of the Notes block, copied from the notebook UI.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of notes to fetch. Defaults to 20. Must be greater than 0 and less than or equal to 20.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Accounts.NotebookBlocks.Notes.Create(AccountID, BlockID, request) -> *pylon.CreateAccountNotebookNoteResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a note in a specific Notes block in an account notebook.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &notebookblocks.AccountsNotebookBlocksNotesCreateRequest{
    AccountID: "account_id",
    BlockID: "block_id",
    ContentHTML: "content_html",
}
client.Accounts.NotebookBlocks.Notes.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**accountID:** `string` — The ID or external ID of the account.
    
</dd>
</dl>

<dl>
<dd>

**blockID:** `string` — The ID of the Notes block, copied from the notebook UI.
    
</dd>
</dl>

<dl>
<dd>

**contentHTML:** `string` — The note body as HTML.
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — An optional title for the note.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CustomFields SelectOptions
<details><summary><code>client.CustomFields.SelectOptions.Create(CustomFieldID, request) -> *pylon.CreateCustomFieldSelectOptionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds an option to a select or multiselect custom field.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &customfields.CustomFieldsSelectOptionsCreateRequest{
    CustomFieldID: "id",
    Label: "label",
    Slug: "slug",
}
client.CustomFields.SelectOptions.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customFieldID:** `string` — The ID of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**aiDescription:** `*string` — The AI description used to help AI-enabled fields select this option.
    
</dd>
</dl>

<dl>
<dd>

**label:** `string` — The display label of the option.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `string` — The API slug stored as the option value.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomFields.SelectOptions.Delete(CustomFieldID) -> *pylon.DeleteCustomFieldSelectOptionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes an option and asynchronously clears it from affected objects.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &customfields.CustomFieldsSelectOptionsDeleteRequest{
    CustomFieldID: "id",
    CurrentSlug: "current_slug",
}
client.CustomFields.SelectOptions.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customFieldID:** `string` — The ID of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**currentSlug:** `string` — The current option slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.CustomFields.SelectOptions.Update(CustomFieldID, request) -> *pylon.UpdateCustomFieldSelectOptionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an option's slug, label, or AI description. Slug changes preserve existing values and migrate persisted filters.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &customfields.CustomFieldsSelectOptionsUpdateRequest{
    CustomFieldID: "id",
    CurrentSlug: "current_slug",
}
client.CustomFields.SelectOptions.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**customFieldID:** `string` — The ID of the custom field.
    
</dd>
</dl>

<dl>
<dd>

**currentSlug:** `string` — The current option slug.
    
</dd>
</dl>

<dl>
<dd>

**aiDescription:** `*string` — A replacement AI description. Pass an empty string to clear it.
    
</dd>
</dl>

<dl>
<dd>

**label:** `*string` — A replacement display label.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — A replacement API slug. Existing object values and persisted filters are migrated to this slug.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## IssueGroups Children
<details><summary><code>client.IssueGroups.Children.Add(IssueGroupID, request) -> *pylon.IssueGroupMutationResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds one or more child issues atomically. Issues already attached to this group are ignored.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issuegroups.IssueGroupsChildrenAddRequest{
    IssueGroupID: "issue_group_id",
    ChildIssueIDs: []string{
        "child_issue_ids",
    },
}
client.IssueGroups.Children.Add(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueGroupID:** `string` — The ID of the issue group.
    
</dd>
</dl>

<dl>
<dd>

**childIssueIDs:** `[]string` — The IDs of the issues to add to the group. At least one is required.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.IssueGroups.Children.Remove(IssueGroupID, ChildIssueID) -> *pylon.IssueGroupMutationResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes one child issue. An issue group must retain at least one child.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issuegroups.IssueGroupsChildrenRemoveRequest{
    IssueGroupID: "issue_group_id",
    ChildIssueID: "child_issue_id",
}
client.IssueGroups.Children.Remove(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueGroupID:** `string` — The ID of the issue group.
    
</dd>
</dl>

<dl>
<dd>

**childIssueID:** `string` — The ID of the child issue to remove.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues Followers
<details><summary><code>client.Issues.Followers.List(IssueID) -> *pylon.GetIssueFollowersResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the list of followers for the specified issue.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesFollowersListRequest{
    IssueID: "id",
}
client.Issues.Followers.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to get followers for.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Followers.Add(IssueID, request) -> *pylon.AddIssueFollowersResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

By default, adds followers. To remove followers, set the operation field to "remove".

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesFollowersAddRequest{
    IssueID: "id",
}
client.Issues.Followers.Add(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue to add followers to.
    
</dd>
</dl>

<dl>
<dd>

**contactIDs:** `[]string` — The IDs of contacts to add as followers.
    
</dd>
</dl>

<dl>
<dd>

**operation:** `*string` — Operation to perform. Use "add" to add followers (default) or "remove" to remove followers.
    
</dd>
</dl>

<dl>
<dd>

**userIDs:** `[]string` — The IDs of users to add as followers.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues Messages
<details><summary><code>client.Issues.Messages.List(IssueID) -> *pylon.GetIssueMessagesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns messages for the specified issue, including replies and internal notes, ordered from oldest to newest.

To post a reply, use the message's top-level id—not thread_id or email_info.message_id. To post an internal note, use an internal thread's thread_id or an internal note's top-level id. Omit both limit and cursor to return all messages; when cursor is provided without limit, the page size defaults to 100.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesMessagesListRequest{
    IssueID: "id",
}
client.Issues.Messages.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue to fetch messages for.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of messages to fetch. Must be greater than 0 and at most 1000. If omitted, all messages are returned for backward compatibility.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Messages.Delete(IssueID, MessageID) -> *pylon.DeleteMessageResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a message from an issue and its connected external system.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesMessagesDeleteRequest{
    IssueID: "id",
    MessageID: "message_id",
}
client.Issues.Messages.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue that the message belongs to.
    
</dd>
</dl>

<dl>
<dd>

**messageID:** `string` — The ID of the message to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Messages.Update(IssueID, MessageID, request) -> *pylon.UpdateMessageResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the body of a message and syncs the edit to its connected channel (Slack, Microsoft Teams, Discord, Google Chat, Telegram, or the chat widget).
Only messages authored by the API token's user can be edited. Emails, customer messages, and redacted messages cannot be edited.
Callers without issue write access can edit only their own internal notes.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesMessagesUpdateRequest{
    IssueID: "id",
    MessageID: "message_id",
    BodyHTML: "body_html",
}
client.Issues.Messages.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue that the message belongs to.
    
</dd>
</dl>

<dl>
<dd>

**messageID:** `string` — The ID of the message to edit.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The new message body in HTML. Replaces the existing body.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Messages.Redact(IssueID, MessageID, request) -> *pylon.RedactMessageResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently replaces a message's stored content with redacted_body_message and optionally deletes its attachments. This action cannot be undone.
When omitted, redacted_body_message defaults to "This message has been redacted." and redact_attachments defaults to true.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesMessagesRedactRequest{
    IssueID: "id",
    MessageID: "message_id",
}
client.Issues.Messages.Redact(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue that the message belongs to.
    
</dd>
</dl>

<dl>
<dd>

**messageID:** `string` — The ID of the message to redact.
    
</dd>
</dl>

<dl>
<dd>

**redactAttachments:** `*bool` — Whether to permanently delete the message's attachments. Defaults to true.
    
</dd>
</dl>

<dl>
<dd>

**redactedBodyMessage:** `*string` — Replacement message body in HTML. The caller is responsible for replacing any sensitive portions. Defaults to "This message has been redacted."
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues SurveyResponses
<details><summary><code>client.Issues.SurveyResponses.List(IssueID) -> *pylon.GetIssueSurveyResponsesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns paginated CSAT and custom survey responses associated with an issue.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesSurveyResponsesListRequest{
    IssueID: "id",
}
client.Issues.SurveyResponses.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID or number of the issue.
    
</dd>
</dl>

<dl>
<dd>

**surveyID:** `*string` — Filter responses by survey template ID.
    
</dd>
</dl>

<dl>
<dd>

**submittedAfter:** `*time.Time` — Filter responses submitted after this time (RFC3339 format).
    
</dd>
</dl>

<dl>
<dd>

**submittedBefore:** `*time.Time` — Filter responses submitted before this time (RFC3339 format).
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of responses to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues Threads
<details><summary><code>client.Issues.Threads.List(IssueID) -> *pylon.GetIssueThreadsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all threads for the specified issue.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesThreadsListRequest{
    IssueID: "id",
}
client.Issues.Threads.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue to fetch threads for.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Issues.Threads.Create(IssueID, request) -> *pylon.CreateIssueThreadResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new internal thread on an issue.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesThreadsCreateRequest{
    IssueID: "id",
}
client.Issues.Threads.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue to create a thread for.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` — The name of the thread.
    
</dd>
</dl>

<dl>
<dd>

**slackChannelID:** `*string` 

The Slack channel ID to sync the thread to. When slack_thread_ts is also provided, links that existing Slack thread. Otherwise, creates a new Slack-backed thread.
Linking an existing Slack thread imports its message history and enables ongoing synchronization. Creating or linking a Slack-backed thread requires an API token configured to act as a human Pylon user whose verified Slack identity is a member of the channel. Pylon bot users and standalone API identities are not supported because they do not have Slack-verifiable channel membership.
    
</dd>
</dl>

<dl>
<dd>

**slackThreadTs:** `*string` — The root message timestamp of an existing Slack thread to link. Requires slack_channel_id.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Issues VoiceCalls
<details><summary><code>client.Issues.VoiceCalls.List(IssueID) -> *pylon.GetIssueVoiceCallsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns voice call records for the specified phone issue. Each call includes its recordings, with parsed transcript segments and a presigned download URL for the audio file. Recordings whose transcript has not yet completed are omitted; refetch later to see them.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &issues.IssuesVoiceCallsListRequest{
    IssueID: "id",
}
client.Issues.VoiceCalls.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**issueID:** `string` — The ID of the issue to fetch voice calls for.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## KnowledgeBases Articles
<details><summary><code>client.KnowledgeBases.Articles.List(KnowledgeBaseID) -> *pylon.GetArticlesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of articles for the specified knowledge base.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesListRequest{
    KnowledgeBaseID: "id",
}
client.KnowledgeBases.Articles.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base the articles are being fetched from.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor to use for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of articles to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>

<dl>
<dd>

**language:** `*string` — The language code to fetch articles in. If not provided, returns the default language.
    
</dd>
</dl>

<dl>
<dd>

**media:** `*knowledgebases.ListArticlesRequestMedia` — Controls whether embedded media is included in article HTML. Valid values are all (default) and none. When set to none, embedded images, video, audio, and inline media are removed while descriptive text and standard links are preserved.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Articles.Create(KnowledgeBaseID, request) -> *pylon.CreateArticleResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new article within a knowledge base.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesCreateRequest{
    KnowledgeBaseID: "id",
    AuthorUserID: "author_user_id",
    Title: "title",
}
client.KnowledgeBases.Articles.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base the article is being added to.
    
</dd>
</dl>

<dl>
<dd>

**authorUserID:** `string` — The ID of the user attributed as the author of the article.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — The HTML body of the article. Required unless body_markdown is set.
    
</dd>
</dl>

<dl>
<dd>

**bodyMarkdown:** `*string` — The body of the article in markdown, instead of body_html.
    
</dd>
</dl>

<dl>
<dd>

**collectionID:** `*string` — The ID of the collection containing the article.
    
</dd>
</dl>

<dl>
<dd>

**isPublished:** `*bool` — Whether the article should be published. Defaults to false.
    
</dd>
</dl>

<dl>
<dd>

**isUnlisted:** `*bool` — Whether the article is accessible only via a direct link. Defaults to false.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — The slug of the article. Defaults to a slug based on the title.
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — The title of the article.
    
</dd>
</dl>

<dl>
<dd>

**translations:** `[]*pylon.ArticleTranslationInput` — Translations of the article content in different languages
    
</dd>
</dl>

<dl>
<dd>

**visibilityConfig:** `*pylon.ArticleVisibilityConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Articles.Get(KnowledgeBaseID, ArticleID) -> *pylon.GetArticleResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single article by ID within the specified knowledge base.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesGetRequest{
    KnowledgeBaseID: "id",
    ArticleID: "article_id",
}
client.KnowledgeBases.Articles.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The KnowledgeBaseID of the article to fetch.
    
</dd>
</dl>

<dl>
<dd>

**articleID:** `string` — The ID of the article to fetch.
    
</dd>
</dl>

<dl>
<dd>

**language:** `*string` — The language code to fetch the article in. If not provided, returns the default language.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Articles.Delete(KnowledgeBaseID, ArticleID) -> *pylon.DeleteArticleResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes an article from the knowledge base.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesDeleteRequest{
    KnowledgeBaseID: "id",
    ArticleID: "article_id",
}
client.KnowledgeBases.Articles.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The KnowledgeBaseID of the article to delete.
    
</dd>
</dl>

<dl>
<dd>

**articleID:** `string` — The ID of the article to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Articles.Update(KnowledgeBaseID, ArticleID, request) -> *pylon.UpdateArticleResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing article. Only provided fields are modified.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesUpdateRequest{
    KnowledgeBaseID: "id",
    ArticleID: "article_id",
}
client.KnowledgeBases.Articles.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The KnowledgeBaseID of the article to update.
    
</dd>
</dl>

<dl>
<dd>

**articleID:** `string` — The ID of the article to update.
    
</dd>
</dl>

<dl>
<dd>

**authorUserID:** `*string` — The ID of the user in this organization attributed as the author of the article. Does not change version authorship.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `*string` — The HTML body of the article. Saved as a new draft; the published article changes only if publish_updated_body_html or is_published is true.
    
</dd>
</dl>

<dl>
<dd>

**bodyMarkdown:** `*string` — The body of the article in markdown, instead of body_html. Saved and published the same way.
    
</dd>
</dl>

<dl>
<dd>

**collectionID:** `*string` — The ID of the collection containing the article.
    
</dd>
</dl>

<dl>
<dd>

**isPublished:** `*bool` — Whether the article should be published or unpublished.
    
</dd>
</dl>

<dl>
<dd>

**isUnlisted:** `*bool` — Whether the article is accessible only via a direct link.
    
</dd>
</dl>

<dl>
<dd>

**language:** `*string` — The language code of the translation to update. If not provided, the default language (original article) will be updated.
    
</dd>
</dl>

<dl>
<dd>

**publishUpdatedBodyHTML:** `*bool` — Whether to publish the updated body_html. Defaults to false, which leaves the change as a draft.
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` — IDs of article tags to assign. If provided, replaces all tags currently assigned to the article.
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — The title of the article. For the default language, applies to the live article immediately.
    
</dd>
</dl>

<dl>
<dd>

**visibilityConfig:** `*pylon.ArticleVisibilityConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Articles.RequestReview(KnowledgeBaseID, ArticleID, request) -> *pylon.RequestArticleReviewResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requests human and/or AI review on the article's current draft version. At least one of `reviewer_user_ids` or `request_ai_review` must be provided. The article must have an unpublished current version. Requesting AI review requires the organization to have AI article review enabled.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesArticlesRequestReviewRequest{
    KnowledgeBaseID: "id",
    ArticleID: "article_id",
}
client.KnowledgeBases.Articles.RequestReview(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base the article belongs to.
    
</dd>
</dl>

<dl>
<dd>

**articleID:** `string` — The ID of the article to request review for.
    
</dd>
</dl>

<dl>
<dd>

**requestAiReview:** `*bool` — When true, also queue an AI review. Requires the organization to have AI article review enabled.
    
</dd>
</dl>

<dl>
<dd>

**reviewerUserIDs:** `[]string` — IDs of users to request a human review from. Each user must already be a configured reviewer for the article's knowledge base.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## KnowledgeBases Collections
<details><summary><code>client.KnowledgeBases.Collections.List(KnowledgeBaseID) -> *pylon.GetCollectionsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all collections for the specified knowledge base.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesCollectionsListRequest{
    KnowledgeBaseID: "id",
}
client.KnowledgeBases.Collections.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Collections.Create(KnowledgeBaseID, request) -> *pylon.CreateCollectionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new collection within a knowledge base.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesCollectionsCreateRequest{
    KnowledgeBaseID: "id",
    Title: "title",
}
client.KnowledgeBases.Collections.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base the article is being added to.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — Description of the collection.
    
</dd>
</dl>

<dl>
<dd>

**parentCollectionID:** `*string` — The ID of the parent collection.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — The slug of the collection. Defaults to a slug based on the title.
    
</dd>
</dl>

<dl>
<dd>

**title:** `string` — The title of the collection.
    
</dd>
</dl>

<dl>
<dd>

**visibilityConfig:** `*pylon.CollectionVisibilityConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Collections.Get(KnowledgeBaseID, CollectionID) -> *pylon.GetCollectionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a single collection by ID within the specified knowledge base.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesCollectionsGetRequest{
    KnowledgeBaseID: "id",
    CollectionID: "collection_id",
}
client.KnowledgeBases.Collections.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base
    
</dd>
</dl>

<dl>
<dd>

**collectionID:** `string` — The ID of the collection
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Collections.Delete(KnowledgeBaseID, CollectionID) -> *pylon.DeleteCollectionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Permanently deletes a collection and all articles within it from the knowledge base. Nested collections and their articles are also deleted.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesCollectionsDeleteRequest{
    KnowledgeBaseID: "id",
    CollectionID: "collection_id",
}
client.KnowledgeBases.Collections.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base that the collection belongs to.
    
</dd>
</dl>

<dl>
<dd>

**collectionID:** `string` — The ID of the collection to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Collections.Update(KnowledgeBaseID, CollectionID, request) -> *pylon.UpdateCollectionResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing collection. Only provided fields are modified.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesCollectionsUpdateRequest{
    KnowledgeBaseID: "id",
    CollectionID: "collection_id",
}
client.KnowledgeBases.Collections.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base that the collection belongs to.
    
</dd>
</dl>

<dl>
<dd>

**collectionID:** `string` — The ID of the collection to update.
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` — The description of the collection.
    
</dd>
</dl>

<dl>
<dd>

**slug:** `*string` — The slug of the collection.
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` — The title of the collection.
    
</dd>
</dl>

<dl>
<dd>

**visibilityConfig:** `*pylon.CollectionVisibilityConfig` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## KnowledgeBases RouteRedirects
<details><summary><code>client.KnowledgeBases.RouteRedirects.Create(KnowledgeBaseID, request) -> *pylon.CreateRouteRedirectResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a path redirect within a knowledge base, mapping a source path to an article or collection.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesRouteRedirectsCreateRequest{
    KnowledgeBaseID: "id",
    FromPath: "from_path",
    ObjectID: "object_id",
    ObjectType: "object_type",
}
client.KnowledgeBases.RouteRedirects.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base the route redirect is being added to.
    
</dd>
</dl>

<dl>
<dd>

**fromPath:** `string` — The path to redirect from.
    
</dd>
</dl>

<dl>
<dd>

**language:** `*string` — Language of the object to redirect to. If not specified, the default language of the knowledge base will be used.
    
</dd>
</dl>

<dl>
<dd>

**objectID:** `string` — The ID of the object to redirect to.
    
</dd>
</dl>

<dl>
<dd>

**objectType:** `string` — The type of the object to redirect to. Must be "article" or "collection".
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## KnowledgeBases Themes
<details><summary><code>client.KnowledgeBases.Themes.Get(KnowledgeBaseID, ThemeID) -> *pylon.GetKnowledgeBaseThemeResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a theme's editable files, including current draft and published content.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesThemesGetRequest{
    KnowledgeBaseID: "id",
    ThemeID: "theme_id",
}
client.KnowledgeBases.Themes.Get(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base.
    
</dd>
</dl>

<dl>
<dd>

**themeID:** `string` — The ID of the theme.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Themes.Update(KnowledgeBaseID, ThemeID, request) -> *pylon.UpdateKnowledgeBaseThemeResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces one or more complete theme files in a single atomic draft update. Use the publish endpoint to make the changes live.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesThemesUpdateRequest{
    KnowledgeBaseID: "id",
    ThemeID: "theme_id",
    Assets: []*pylon.UpdateKnowledgeBaseThemeAsset{
        &pylon.UpdateKnowledgeBaseThemeAsset{
            AssetType: "asset_type",
            Content: "content",
        },
    },
}
client.KnowledgeBases.Themes.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base.
    
</dd>
</dl>

<dl>
<dd>

**themeID:** `string` — The ID of the theme.
    
</dd>
</dl>

<dl>
<dd>

**assets:** `[]*pylon.UpdateKnowledgeBaseThemeAsset` — The complete theme files to replace. Changes are saved as drafts and are not published.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.KnowledgeBases.Themes.Publish(KnowledgeBaseID, ThemeID) -> *pylon.PublishKnowledgeBaseThemeResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Promotes all current draft files to their published versions. Changes become live immediately when this is the knowledge base's active theme. Publishing a theme with no draft changes is a no-op.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &knowledgebases.KnowledgeBasesThemesPublishRequest{
    KnowledgeBaseID: "id",
    ThemeID: "theme_id",
}
client.KnowledgeBases.Themes.Publish(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**knowledgeBaseID:** `string` — The ID of the knowledge base.
    
</dd>
</dl>

<dl>
<dd>

**themeID:** `string` — The ID of the theme.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Surveys Responses
<details><summary><code>client.Surveys.Responses.List(SurveyID) -> *pylon.GetSurveyResponsesResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns paginated survey responses visible to the caller, optionally filtered by time range, account, or contact.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &surveys.SurveysResponsesListRequest{
    SurveyID: "id",
}
client.Surveys.Responses.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**surveyID:** `string` — The ID of the survey.
    
</dd>
</dl>

<dl>
<dd>

**submittedAfter:** `*time.Time` — Filter responses submitted after this time (RFC3339 format).
    
</dd>
</dl>

<dl>
<dd>

**submittedBefore:** `*time.Time` — Filter responses submitted before this time (RFC3339 format).
    
</dd>
</dl>

<dl>
<dd>

**accountID:** `*string` — Filter responses by account ID. Required with contact_id when the caller has scoped account or contact access.
    
</dd>
</dl>

<dl>
<dd>

**contactID:** `*string` — Filter responses by contact ID. Required with account_id when the caller has scoped account or contact access.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `*string` — The cursor for pagination.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int64` — The number of responses to fetch. Defaults to 100. Must be greater than 0 and less than 1000.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tasks Comments
<details><summary><code>client.Tasks.Comments.List(TaskID) -> *pylon.GetTaskCommentsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns all comments for a task, ordered by creation time.

**Rate limit:** 300 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &tasks.TasksCommentsListRequest{
    TaskID: "id",
}
client.Tasks.Comments.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task to fetch comments for.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Comments.Create(TaskID, request) -> *pylon.CreateTaskCommentResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new comment on a task. The authenticated user is the author.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &tasks.TasksCommentsCreateRequest{
    TaskID: "id",
    BodyHTML: "body_html",
}
client.Tasks.Comments.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task to add a comment to.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The body of the comment in HTML format.
    
</dd>
</dl>

<dl>
<dd>

**isInternal:** `*bool` — Whether the comment is visible only to internal users.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Comments.Delete(TaskID, CommentID) -> *pylon.DeleteTaskCommentResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes an existing comment. Only the original author can delete their comment.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &tasks.TasksCommentsDeleteRequest{
    TaskID: "id",
    CommentID: "comment_id",
}
client.Tasks.Comments.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task.
    
</dd>
</dl>

<dl>
<dd>

**commentID:** `string` — The ID of the comment to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tasks.Comments.Update(TaskID, CommentID, request) -> *pylon.UpdateTaskCommentResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing comment. Only the original author can update their comment.

**Rate limit:** 120 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &tasks.TasksCommentsUpdateRequest{
    TaskID: "id",
    CommentID: "comment_id",
    BodyHTML: "body_html",
}
client.Tasks.Comments.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**taskID:** `string` — The ID of the task.
    
</dd>
</dl>

<dl>
<dd>

**commentID:** `string` — The ID of the comment to update.
    
</dd>
</dl>

<dl>
<dd>

**bodyHTML:** `string` — The updated body of the comment in HTML format.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TrainingData Documents
<details><summary><code>client.TrainingData.Documents.Delete(TrainingDataID) -> *pylon.DeleteTrainingDataDocumentsResponseBody</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes documents from a training data configuration by document ID or external ID.

**Rate limit:** 30 requests per minute
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &trainingdata.TrainingDataDocumentsDeleteRequest{
    TrainingDataID: "id",
}
client.TrainingData.Documents.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**trainingDataID:** `string` — The ID of the training data.
    
</dd>
</dl>

<dl>
<dd>

**documentIDs:** `*string` — Document IDs to delete.
    
</dd>
</dl>

<dl>
<dd>

**externalIDs:** `*string` — External IDs to delete.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

