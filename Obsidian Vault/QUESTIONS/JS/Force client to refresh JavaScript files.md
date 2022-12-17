As far as I know a common solution is to add a `?<version>` to the script's src link.

For instance:

```javascript
<script type="text/javascript" src="myfile.js?1500"></script>
```

---

> I assume at this point that there isn't a better way than find-replace to increment these "version numbers" in all of the script tags?

You might have a version control system do that for you? Most version control systems have a way to automatically inject the revision number on check-in for instance.

It would look something like this:

```javascript
<script type="text/javascript" src="myfile.js?$$REVISION$$"></script>
```