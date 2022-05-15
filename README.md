# Server Mail

Send emails on server notifications and your customized contents.

## Getting started

Clone this repo and change the directory via

```bash
git clone https://github.com/LittleYe233/server_mail.git
cd server_mail/server_mail
```

Open up your terminal and launch Python interpreter, or create a new Python file, then

```python
from server_mail import BUILTIN_STYLE, minify_content, compose_content, compose_email, send_email
from email.headerregistry import Address

# (display_name, username, domain)
sender = Address('Sender', 'sender', 'example.ltd')
# It's useful for some email servers (like maddy), for their email accounts
# should be the full email address.
sender_account = 'sender@example.ltd'
sender_password = '********************************'
recipients = [
    Address('Recipient 1', 'recipient1', 'example.ltd'),
    Address('Recipient 2', 'recipient2', 'example.ltd')
]

# Compose HTML content
# It's better to use raw strings.
content_md = r'''# Test email from server

This is a test email via `server_mail`.

Visit [LittleYe233/server_mail](https://github.com/LittleYe233/server_mail) for further information.
'''
content = minify_content(compose_content(content_md, BUILTIN_STYLE))

# Compose email
mail = compose_email(
    subject='Test email from server',   # subject
    recipients=recipients,              # recipients
    content=content,                    # HTML content (body) of email
    content_type='html',                # type of conent (here is HTML)
    msg_level='DEBUG',                  # message level (shown in subject)
    sender=sender                       # sender
)

# Send email
# Use SSL/TLS (port 465) as default
send_email(sender_account, sender_password, mail, sender)
```
