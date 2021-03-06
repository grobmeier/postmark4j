# postmark4j

NOTE: meanwhile there is an official library from Postmarkapp, you should consider this instead: https://github.com/wildbit/postmark-java

postmark4j is a community driven effort to work with the Postmarkapp REST API.
It was initially created by Jared Holdcroft.

Please note, this project does not support the full API, only the most important
aspects as sending emails. If you need something done, feel free to send a PR.

## Installation

It's best to install it using Maven:

```
<dependency>
  <groupId>de.grobmeier</groupId>
  <artifactId>postmark4j</artifactId>
  <version>1.1.1</version>
</dependency>
```

## Example usage

```java
List<NameValuePair> headers = new ArrayList<NameValuePair>();

headers.add(new NameValuePair("HEADER", "test"));

PostmarkMessage message = new PostmarkMessage("TO_ADDRESS",
        "FROM_ADDRESS",
        "REPLY_TO_ADDRESS",
        null,
        "SUBJECT",
        "CONTENT",
        false,
        null,
        headers);

PostmarkClient client = new PostmarkClient("POSTMARK_API_TEST");

try {
       client.sendMessage(message);
} catch (PostmarkException pe) {
       System.out.println("An error has occured : " + pe.getMessage());
}
```

Attachments can also be sent:

```java
Attachment attachment = new Attachment();
attachment.setContentType("application/pdf");
attachment.setName("SomethingAwesome.pdf");

// convert file contents to base64
File file = new File("SomethingAwesome.pdf");
byte[] ba = new byte[(int) file.length()];
FileInputStream fis = new FileInputStream(file);
Fileis.read(ba);
fis.close();
attachment.setContent(new Base64().encodeToString(ba));

// can handle multiple attachments
Vector<Attachment> v = new Vector<Attachment>();
v.add(attachment);
message.setAttachments(v);
```

### License:

Copyright (C) 2012 Jared Holdcroft

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
