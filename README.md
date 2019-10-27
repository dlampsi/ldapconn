# ldapconn

[![GoDoc](https://godoc.org/github.com/dlampsi/ldapconn?status.svg)](https://godoc.org/github.com/dlampsi/ldapconn) [![Actions Status](https://github.com/dlampsi/ldapconn/workflows/default/badge.svg)](https://github.com/dlampsi/ldapconn/actions)

Go module for LDAP server operations: search, delete, add and modify LDAP entries.

## Usage

```go
import "github.com/dlampsi/ldapconn"
```

Create new client

```go
cfg := &ldapconn.Config{
    Host:     "dummy.host.com",
    Port:     "636",
    SSL:      true,
    Insecure: false,
    BindDN:   "fakebinduser",
    BindPass: "fakepass",
}

cl, err := ldapconn.NewClient(cfg)
if err != nil {
    // Process err
}
```

Search for user entry in AD:

```go
// Create search request entry
searchBase = "DC=dummy,DC=org,DC=com"
searchFilter := "(sAMAccountName=existsUser)"
searchRequest := cl.CreateRequest(searchBase, searchFilter)

// Perfrom search one entry
ldapEntry, err := cl.SearchEntry(searchRequest)
if err != nil {
    // Process err
}
if ldapEntry == nil {
    // Process not found entry
}

fmt.Println(ldapEntry.GetAttributeValue("cn"))
```