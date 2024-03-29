# OpenSMTPdAdmin

This is a administration interface for OpenSMTPd based mailing systems and the corresponding applications (e.g. IMAP server, like Dovecot). You can edit your domains, your virtual users, their passwords and basic attributes. You can manage aliases pointing into your domain users, or outside. You can also send emails, however it is not thoroughly tested (and probably not the most wanted feature). Your users can change their passwords.

Fork of OpenSMTPdAdmin of high5.nl (and, thus, PostfixAdmin, of course).

## Features

Compared to high5.nl's OpenSTMPdAdmin, here you get more security related functionality and a few simplification:

 - 2FA is enforced for admins. You can enable TOTP based 2FA authentication. Any authenticator application (Google authenticator, Microsoft Authenticator, LastPass, etc.) could be used, the QR code is generated by a javascript (= it is generated at client side). 
   
 - Passwords are measured with enthropy: to avoid users from picking simple passwords, the enhropy of the entered character string is computed and shown. Repeating patterns decrease enthropy remarkably. Try it.

 - Based on SQLite (no need for DB server around). 

 - Extended logging: all security related operations, like login, logoff, password change, etc., plus all activities (all changes) are logged into the database. Logs can be seen on the user interface as well.

## Reasoning

 - You should not use any internet facing administration interface, where 2FA is not enabled. Every service suffers extremely high number of login attempts, passwords do not protect you!

 - If someone uses only small alphabet and the length is at least 30 characters, no one can blame! The idiot requirement of "must have" capitals, digits and special characters leads to nowhere. Use whatever you want, but keep it long! Size does matter!

 - SQLite is absolutely useable for such small scale applications, there is no need to operate (manage and maintain) a database server for this purpose. Play with your kids instead! OpenSMTPd on the other hand comes without MariaDB support (you can recompile, though), thus SQLite is more convenient from the mailer daemon point of view as well. 

 - Logging of the original software was absolutely poor. Nowadays you want to know what happened, logging is the most basic functionality, one can expect from a software like this.
