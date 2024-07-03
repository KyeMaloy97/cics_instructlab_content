The GNTRAN system initialization parameter specifies the transaction that you want CICS to invoke when a
user's terminal-timeout period expires, and instructs CICS whether to keep a pseudo-conversation in use
at a terminal that is the subject of a timeout sign-off.
GNTRAN=({NO|transaction_id}[,{KEEP|DISCARD}])
Valid values are as follows:
NO
The default value, NO, specifies that no special transaction is to be executed when the timeout
period expires. Instead, the user is signed off (subject to the SIGNOFF attribute of the TYPETERM
resource definition for the terminal, as described below). After the signoff, if the LOGONMSG(YES)
option is specified in the TYPETERM resource definition for the terminal, the transaction specified
in the GMTRAN system initialization parameter is executed.
transaction_id
The name of a timeout transaction to sign off the user at the timed-out terminal. You can specify
CESF as the timeout transaction. Specifying your own transaction allows you to specify functions
in addition to, or instead of, sign-off. For example, your own transaction could issue a prompt for
the terminal user's password, and allow the session to continue if the correct password is entered.
The transaction to be used must have been specially written to handle the GNTRAN COMMAREA
that is passed to it. Of the CICS-supplied transactions, only CESF has been written to handle the
GNTRAN COMMAREA. For more information about writing your own transactions for GNTRAN, see
Writing a good night program.
KEEP
CICS attempts to keep a pseudo-conversation at the terminal that is the subject of the timeout.
In this case, CICS performs a read terminal buffer operation, which must succeed if details of a
pseudo-conversation are to be recorded and resumed later.
If the read terminal buffer operation cannot complete (for example, because the terminal
does not respond to communication), the timeout transaction can be interrupted and can wait
unnecessarily.


#### DISCARD
CICS does not attempt to keep a pseudo-conversation at the terminal that is the subject of the
timeout, and does not perform any read terminal buffer operation. Use of XRF is not supported
with this option.
Note: When either the CICS CESF transaction, or your own transaction, attempts to sign off a terminal,
the result is subject to the SIGNOFF attribute of the TYPETERM resource definition for the terminal, as
follows:
SIGNOFF
Effect
YES
The terminal is signed off, but not logged off.
NO
The terminal remains signed on and logged on.
LOGOFF
The terminal is both signed off and logged off.

Note: If GNTRAN fails to attach, and SIGNOFF(LOGOFF) has been specified, the terminal which has
reached timeout will be signed off and logged off. GNTRAN will not run and will have no effect.
