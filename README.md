go-mailutil
====================

Go library with utility functions for extracting information from email messages (using
net/mail's Message type).


Usage
--------------------

    import (
           "mailutil"
           "net/mail"
           "strings"
    )
    
    ...
    
    var mime = "Message-ID: 12a34\r\nTo: a@a.com\r\nCc: b@b.com\r\nSubject: mySubject\r\nDate: Tue, 1 Jul 2003 10:52:37 +0200\r\nContent-Type: multipart/alternative; boundary=f46d043c80b4d7a9b904bce66840\r\n\r\n--f46d043c80b4d7a9b904bce66840\r\nContent-Type: text/plain; charset=UTF-8\r\n\r\nhello this is text\r\n--f46d043c80b4d7a9b904bce66840\r\nContent-Type: text/html; charset=UTF-8\r\nContent-Transfer-Encoding: quoted-printable\r\n\r\n<p>E=3Dmc^2</p>\r\n--f46d043c80b4d7a9b904bce66840\r\n"

    msg, _ := mail.ReadMessage(strings.NewReader(mime))

    text, _ := mailutil.TextBody(msg)
    // text now contains "hello this is text"

    html, _ := mailutil.HTMLBody(msg)
    // html now contains "<p>E=mc^2</p>"


Links
--------------------

* Some of the email multipart MIME parsing code was adapted from
  https://github.com/bradfitz/websomtep/blob/master/websomtep.go.
