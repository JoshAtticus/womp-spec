# Open Graph Link Previews
Open Graph Link Previews allow users to see information about URLs before opening them. This is an **optional** feature of the womp specification.

![Link Preview](../assets/opengraph.png)

A free and publically available link preview API is provided by JoshAtticus, or you can use your own:

```
GET https://og.joshattic.us/fetch?url=https://github.com&t=3759146558600182
```

```json
{
  "requested_url": "https://github.com",
  "status_code": 200,
  "fetched_at_unix": 1797772800,
  "metadata": {
    "title": "GitHub...",
    "description": "...",
    "image": "...",
    "url": "..."
  },
  "cached": false
}
```

You can also optionally choose to allow users to enable/disable open graph link previews when posting. This setting should be attached to the post's womp metadata (see above). Even if your client does not allow users to toggle this on and off, it should still respect this setting in posts if present to maintain womp-compatibility.