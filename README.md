# Pylon Go SDK

The official Go SDK for the [Pylon API](https://docs.usepylon.com).

> **Alpha.** The SDK is new and its interface may change between `v0.x` releases.

## Installation

```bash
go get github.com/pylon-labs/pylon-go
```

Requires Go 1.22 or later.

## Usage

```go
package main

import (
	"context"
	"fmt"
	"os"

	pylonclient "github.com/pylon-labs/pylon-go/client"
	"github.com/pylon-labs/pylon-go/option"
)

func main() {
	ctx := context.Background()
	client := pylonclient.NewClient(option.WithToken(os.Getenv("PYLON_API_TOKEN")))

	me, err := client.Me.Get(ctx)
	if err != nil {
		panic(err)
	}
	fmt.Println(me.GetData().GetName())
}
```

Pylon accounts live in either the US or the EU region, and the client defaults to the US. EU accounts must select the EU region:

```go
import pylon "github.com/pylon-labs/pylon-go"

client := pylonclient.NewClient(
	option.WithToken(os.Getenv("PYLON_API_TOKEN")),
	option.WithBaseURL(pylon.Environments.Eu),
)
```

### Pagination

List and search methods return a page whose iterator fetches the next page as you go:

```go
page, err := client.Accounts.List(ctx, &pylon.AccountsListRequest{Limit: pylon.Int64(100)})
if err != nil {
	return err
}
iter := page.Iterator()
for iter.Next(ctx) {
	fmt.Println(iter.Current().GetName())
}
if err := iter.Err(); err != nil {
	return err
}
```

### Errors

Requests that fail return an error you can match by status, such as `*pylon.NotFoundError`:

```go
_, err := client.Issues.Get(ctx, &pylon.IssuesGetRequest{ID: "issue_id"})
var notFound *pylon.NotFoundError
if errors.As(err, &notFound) {
	fmt.Println("Issue not found")
}
```

### Retries and timeouts

Rate-limited (`429`), timed-out (`408`), and server error (`5xx`) responses are retried with backoff. Requests that create something aren't retried, so a retry can't create a duplicate. Use `option.WithMaxAttempts` or `option.WithoutRetries()` on the client or a single call, and set timeouts through the `context` you pass in.

## Reference

[reference.md](reference.md) documents every method. The [Pylon API documentation](https://docs.usepylon.com) covers the underlying endpoints.

## Contributing

This SDK is generated from Pylon's OpenAPI spec, so changes outside the hand-maintained files listed in `.fernignore` are overwritten by the next sync. Please open an issue for bugs or missing endpoints.
