# Astrocoders-guerrillamail
Node library for interacting with Guerrilla Mail - creates and checks temporary mailboxes

Credits to https://github.com/RedRiverSoftware/rr-guerrillamail

Quick example
-------------
```
// create a temporary email mailbox
const mailbox = new TempMailbox()

// get the address
mailbox.getEmailAddress()
	.then(addr => { console.log('email addr: ' + addr) })
	.then(() => {
		// wait for an email matching the subject
		// in this example, send a message with subject containing "test" to the displayed address
		return mailbox.waitForEmail(m => {
			return (m.mail_subject.indexOf('test') !== -1)
		})
	})
	.then(mail => {
		// log out the entire object of the email which matched
		// including mail_body, which is the content
		console.log(JSON.stringify(mail, null, 2))
		
		// delete the resulting email
		mailbox.deleteMail(mail.mail_id)
	})
```
