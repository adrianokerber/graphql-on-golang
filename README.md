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
create table courses (id string, name string, description string, category_id string);
## Optional commands:
# Query data
select * from categories;
# Clear table
delete from categories;
# List table columns
pragma table_info(courses);
# Join tables to search by a course with its category
select * from courses cou inner join categories cat on cat.id = cou.category_id where cou.id = 'e7e66f27-7b39-4ee0-a5e6-a7e9a97d40ca';
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

mutation createCourse {
  createCourse(input:{name: "Full Cycle", description: "The best!", categoryId: "a639f82e-d442-4554-8a07-072ec327b13c"}){
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
  }
}

query queryCategoriesWithCourses {
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

query queryCourses {
  courses {
    id
    name
  }
}

query queryCoursesWithCategory {
  courses {
    id
    name
    description
    category {
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