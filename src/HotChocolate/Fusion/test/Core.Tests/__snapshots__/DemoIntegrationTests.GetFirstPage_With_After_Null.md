# GetFirstPage_With_After_Null

## User Request

```graphql
query AfterNull($after: String) {
  appointments(after: $after) {
    nodes {
      id
    }
  }
}
```

## Result

```json
{
  "data": {
    "appointments": {
      "nodes": [
        {
          "id": "QXBwb2ludG1lbnQ6MQ=="
        },
        {
          "id": "QXBwb2ludG1lbnQ6Mg=="
        }
      ]
    }
  }
}
```

## QueryPlan

```json
{
  "document": "query AfterNull($after: String) { appointments(after: $after) { nodes { id } } }",
  "operation": "AfterNull",
  "rootNode": {
    "type": "Sequence",
    "nodes": [
      {
        "type": "Resolve",
        "subgraph": "Appointment",
        "document": "query AfterNull_1($after: String) { appointments(after: $after) { nodes { id } } }",
        "selectionSetId": 0,
        "forwardedVariables": [
          {
            "variable": "after"
          }
        ]
      },
      {
        "type": "Compose",
        "selectionSetIds": [
          0
        ]
      }
    ]
  }
}
```

## QueryPlan Hash

```text
C601EB39A2F136D152B59B30853A0073588356FE
```

## Fusion Graph

```graphql
schema
  @fusion(version: 1)
  @transport(subgraph: "Appointment", location: "http:\/\/localhost:5000\/graphql", kind: "HTTP")
  @transport(subgraph: "Appointment", location: "ws:\/\/localhost:5000\/graphql", kind: "WebSocket")
  @node(subgraph: "Appointment", types: [ "Patient1", "Appointment" ]) {
  query: Query
}

type Query {
  appointmentById(appointmentId: ID!): Appointment
    @variable(subgraph: "Appointment", name: "appointmentId", argument: "appointmentId")
    @resolver(subgraph: "Appointment", select: "{ appointmentById(appointmentId: $appointmentId) }", arguments: [ { name: "appointmentId", type: "ID!" } ])
  appointments("Returns the elements in the list that come after the specified cursor." after: String "Returns the elements in the list that come before the specified cursor." before: String "Returns the first _n_ elements from the list." first: Int "Returns the last _n_ elements from the list." last: Int): AppointmentsConnection
    @variable(subgraph: "Appointment", name: "after", argument: "after")
    @variable(subgraph: "Appointment", name: "before", argument: "before")
    @variable(subgraph: "Appointment", name: "first", argument: "first")
    @variable(subgraph: "Appointment", name: "last", argument: "last")
    @resolver(subgraph: "Appointment", select: "{ appointments(after: $after, before: $before, first: $first, last: $last) }", arguments: [ { name: "after", type: "String" }, { name: "before", type: "String" }, { name: "first", type: "Int" }, { name: "last", type: "Int" } ])
  "Fetches an object given its ID."
  node("ID of the object." id: ID!): Node
    @variable(subgraph: "Appointment", name: "id", argument: "id")
    @resolver(subgraph: "Appointment", select: "{ node(id: $id) }", arguments: [ { name: "id", type: "ID!" } ])
  "Lookup nodes by a list of IDs."
  nodes("The list of node IDs." ids: [ID!]!): [Node]!
    @variable(subgraph: "Appointment", name: "ids", argument: "ids")
    @resolver(subgraph: "Appointment", select: "{ nodes(ids: $ids) }", arguments: [ { name: "ids", type: "[ID!]!" } ])
  patient(id: ID!): Patient1
    @variable(subgraph: "Appointment", name: "id", argument: "id")
    @resolver(subgraph: "Appointment", select: "{ patient(id: $id) }", arguments: [ { name: "id", type: "ID!" } ])
}

type Appointment implements Node
  @variable(subgraph: "Appointment", name: "Appointment_id", select: "id")
  @resolver(subgraph: "Appointment", select: "{ appointmentById(appointmentId: $Appointment_id) }", arguments: [ { name: "Appointment_id", type: "ID!" } ])
  @resolver(subgraph: "Appointment", select: "{ nodes(ids: $Appointment_id) { ... on Appointment { ... Appointment } } }", arguments: [ { name: "Appointment_id", type: "[ID!]!" } ], kind: "BATCH") {
  id: ID!
    @source(subgraph: "Appointment")
  patient: IPatient!
    @source(subgraph: "Appointment")
}

"A connection to a list of items."
type AppointmentsConnection {
  "A list of edges."
  edges: [AppointmentsEdge!]
    @source(subgraph: "Appointment")
  "A flattened list of the nodes."
  nodes: [Appointment!]
    @source(subgraph: "Appointment")
  "Information to aid in pagination."
  pageInfo: PageInfo!
    @source(subgraph: "Appointment")
}

"An edge in a connection."
type AppointmentsEdge {
  "A cursor for use in pagination."
  cursor: String!
    @source(subgraph: "Appointment")
  "The item at the end of the edge."
  node: Appointment!
    @source(subgraph: "Appointment")
}

"Information about pagination in a connection."
type PageInfo {
  "When paginating forwards, the cursor to continue."
  endCursor: String
    @source(subgraph: "Appointment")
  "Indicates whether more edges exist following the set defined by the clients arguments."
  hasNextPage: Boolean!
    @source(subgraph: "Appointment")
  "Indicates whether more edges exist prior the set defined by the clients arguments."
  hasPreviousPage: Boolean!
    @source(subgraph: "Appointment")
  "When paginating backwards, the cursor to continue."
  startCursor: String
    @source(subgraph: "Appointment")
}

type Patient1 implements IPatient & Node
  @variable(subgraph: "Appointment", name: "Patient1_id", select: "id")
  @resolver(subgraph: "Appointment", select: "{ node(id: $Patient1_id) { ... on Patient1 { ... Patient1 } } }", arguments: [ { name: "Patient1_id", type: "ID!" } ])
  @resolver(subgraph: "Appointment", select: "{ nodes(ids: $Patient1_id) { ... on Patient1 { ... Patient1 } } }", arguments: [ { name: "Patient1_id", type: "[ID!]!" } ], kind: "BATCH") {
  appointments("Returns the elements in the list that come after the specified cursor." after: String "Returns the elements in the list that come before the specified cursor." before: String "Returns the first _n_ elements from the list." first: Int "Returns the last _n_ elements from the list." last: Int): AppointmentsConnection
    @source(subgraph: "Appointment")
    @variable(subgraph: "Appointment", name: "after", argument: "after")
    @variable(subgraph: "Appointment", name: "before", argument: "before")
    @variable(subgraph: "Appointment", name: "first", argument: "first")
    @variable(subgraph: "Appointment", name: "last", argument: "last")
  id: ID!
    @source(subgraph: "Appointment")
}

type Patient2 implements IPatient {
  id: ID!
    @source(subgraph: "Appointment")
}

interface IPatient {
  id: ID!
}

"The node interface is implemented by entities that have a global unique identifier."
interface Node {
  id: ID!
}
```

