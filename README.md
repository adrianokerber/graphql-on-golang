# graphql-on-golang
Simple project using Graphql with Go.

## Useful commands
Useful commands to use.

Install Go dependencies:
```
go mod tidy
```

Configure local database
```bash
# Install database sqlite3 (On Linux)
sudo apt install sqlite3

# Enter on database
sqlite3 data.db
# Create tables
create table categories (id string, name string, description string);
# Query data
select * from categories;
```
> Important: in order to exit database CLI type `.quit`. Unless you were already typping a command then type `;` to finish it first.

Start our GraphQL server:
```bash
go run cmd/server/server.go
```

Update GraphQL schemas using:
```bash
go run github.com/99designs/gqlgen generate
```

## Queries and Mutations
Samples of queries and mutations to teste on the API

```graphql
mutation createCategory {
  createCategory(input: {name: "Tecnologia", description: "Cursos de Tecnologia"}){
    id
    name
    description
  }
}

query queryCategories {
  categories {
    id
    name
    description
    courses {
      id
      name
      description
    }
  }
}
```

## Common issues
A list of common issues of day by day development.

---
Issue:
`"Binary was compiled with 'CGO_ENABLED=0', go-sqlite3 requires cgo to work. This is a stub"`

Solution:
Set variable CGO_ENABLED to 1 and run go build
```bash
export CGO_ENABLED=1
go build
```
---

## Dependencies
- [gqlgen](https://gqlgen.com/)
- [sqlite](https://www.sqlite.org/index.html)