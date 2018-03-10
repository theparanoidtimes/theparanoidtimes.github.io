---
layout: page
title: tabellarium
category: projects
project-repo: https://github.com/theparanoidtimes/tabellarium
---

*tabellarium* allows you to execute various task agains an e-mail mailbox.
Example for this is processing all messages in the inbox in order to find
messages with specific text or collect all attachments or anything similar.

Bring the code!

```java
MailboxTaskExecutor executor = new ImapMailboxFolderTaskExecutor
    ("user@host", "username", "password", "folderName");
```
The above code creates an executor instance that will execute tasks against
one folder of the mailbox. Currently only *IMAP* protocol is supported.

In order to process messages in the folder you need to supply a handler
to the executor like this:
```java
mailboxTaskExecutor.executeForEachEmail(message -> {
    System.out.println(message.getSubject());
});

// There is a built-in handler for printing out the whole message.
executor.executeForEachEmail(new PrintingEmailHandler(System.out));
```

For more info see the [repo]({{ page.project-repo }}).
