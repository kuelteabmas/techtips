# Java Clean Code - Sonarlint
---
### Sonarlint Java:S2259 - Null pointers should not be dereferenced

Sonarlint will occur at `response.getBody.getMessage()` due to it causing a NullPointerException because either: 

* `response` is null.
* `response.getBody()` returns null when calling getStatus().

To prevent dereferencing a null object, you should first check if the relevant objects are non-null before accessing their methods or properties.

A for-sure solution is the following:

Non-compliant Code:
```
if (response != null && response.getBody() != null) {
    response.getBody.getMessage();
}
```

Compliant Code:
```
ResponseObject responseBody = response.getBody();

if (response != null && responseBody != null) {
    response.getBody.getMessage();
}
```

---