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


Get download url of latest restic release
-----------------------------------------

```
# curl -s 'https://api.github.com/repos/restic/restic/releases/latest' | jq -r '.assets[] | select(.name | match("^restic_.*_linux_amd64\\.bz2$")) | .browser_download_url'
https://github.com/restic/restic/releases/download/v0.16.5/restic_0.16.5_linux_amd64.bz2

# curl -s 'https://api.github.com/repos/restic/restic/releases/latest' | jq -r '.assets[] | select(.name | contains("linux_amd64")) | .browser_download_url'
https://github.com/restic/restic/releases/download/v0.16.5/restic_0.16.5_linux_amd64.bz2
