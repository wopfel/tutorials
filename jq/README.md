jq examples
===========

See the great jq tool at https://github.com/stedolan/jq.

```json

{
  "points": [
    {
      "id": "123",
      "title": "One",
      "data1": "",
      "data2": "",
      "outlets": [
        {
          "uid": "1",
          "health": "okay",
          "type": "node"
        },
        {
          "uid": "2",
          "health": "okay",
          "type": "node"
        }
      ]
    },
    {
      "id": "456",
      "title": "Two",
      "data1": "",
      "data2": "",
      "outlets": [
        {
          "uid": "11",
          "health": "okay",
          "type": "node"
        },
        {
          "uid": "12",
          "health": "okay",
          "type": "node"
        }
      ]
    }
  ]
}

```

The title field is written only once. Outlets is an array:

```
# jq '.points[] | select(.id == "456") | { title: .title , outlets: .outlets }' < sample-001.json

{
  "title": "Two",
  "outlets": [
    {
      "uid": "11",
      "health": "okay",
      "type": "node"
    },
    {
      "uid": "12",
      "health": "okay",
      "type": "node"
    }
  ]
}
```

Title is repeated for every object. No array at all:

```
# jq '.points[] | select(.id == "456") | { title: .title , outlets: .outlets[] }' < sample-001.json
{
  "title": "Two",
  "outlets": {
    "uid": "11",
    "health": "okay",
    "type": "node"
  }
}
{
  "title": "Two",
  "outlets": {
    "uid": "12",
    "health": "okay",
    "type": "node"
  }
}
```
