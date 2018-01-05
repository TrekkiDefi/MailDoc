## NAME

smtp-source - 并行的 SMTP/LMTP 测试生成器

## SYNOPSIS

smtp-source [options] [inet:]host[:port]
smtp-source [options] unix:pathname

## DESCRIPTION

smtp-source连接到指定的主机和TCP端口（默认：端口25），并向它发送一个或多个消息，无论是按顺序还是并行。
该程序使用SMTP（默认）或LMTP。可以连接到UNIX域和IPv4或IPv6服务器 IPv4和IPv6是默认的。

### Arguments:
- -4     Connect to the server with IPv4. This option has no effect  when
      Postfix is built without IPv6 support.

- -6     Connect  to  the  server with IPv6. This option is not available
      when Postfix is built without IPv6 support.

- -A     Don't abort when the  server  sends  something  other  than  the
      expected positive reply code.

- -c     Display  a running counter that is incremented each time an SMTP
      DATA command completes.

- -C count
      When a host sends RESET instead  of  SYN|ACK,  try  count  times
      before giving up. The default count is 1. Specify a larger count
      in order to work around a problem with TCP/IP stacks  that  send
      RESET when the listen queue is full.

- -d     Don't  disconnect after sending a message; send the next message
      over the same connection.

- -f from
      Use the specified sender address (default: <foo@myhostname>).

- -F file
      Send the pre-formatted message header and body in the  specified
      file, while prepending '.' before lines that begin with '.', and
      while appending CRLF after each line.

- -l length
      Send length bytes  as  message  payload.  The  length  does  not
      include message headers.

- -L     Speak LMTP rather than SMTP.

- -m message_count
      Send the specified number of messages (default: 1).

- -M myhostname
      Use  the specified hostname or [address] in the HELO command and
      in the default sender and recipient addresses,  instead  of  the
      machine hostname.

- -N     Prepend  a  non-repeating  sequence  number  to  each  recipient
      address. This avoids the artificial 100% hit rate in the resolve
      and rewrite client caches and exercises the trivial-rewrite dae-
      mon, better approximating Postfix  performance  under  real-life
      work-loads.

- -o     Old mode: don't send HELO, and don't send message headers.

- -r recipient_count
      Send   the   specified  number  of  recipients  per  transaction
      (default: 1).  Recipient names are  generated  by  prepending  a
      number to the recipient address.

- -R interval
      Wait for a random period of time 0 <= n <= interval between mes-
      sages.  Suspending one thread does  not  affect  other  delivery
      threads.

- -s session_count
      Run  the specified number of SMTP sessions in parallel (default:
      1).

- -S subject
      Send mail with the named subject line (default: none).

- -t to  Use the specified recipient address (default: <foo@myhostname>).

- -T windowsize
      Override  the default TCP window size. To work around broken TCP
      window scaling implementations, specify a value > 0 and < 65536.

- -v     Make the program more verbose, for debugging purposes.

- -w interval
      Wait  a fixed time between messages.  Suspending one thread does
      not affect other delivery threads.

- [inet:]host[:port]
      Connect via TCP to host host, port port.  The  default  port  is
      smtp.

- unix:pathname
      Connect to the UNIX-domain socket at pathname.
## BUGS

No SMTP command pipelining support.

## SEE ALSO

[smtp-sink(1)](http://www.postfix.org/smtp-sink.1.html), SMTP/LMTP message dump
