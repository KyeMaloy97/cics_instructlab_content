## Chapter 1. System initialization parameter summary

```
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
For details, see Specifying CICS system initialization parameters and the linked description of each
parameter.
For a summary of changes, by release of CICS, to SIT parameters, see Changes to SIT parameters.
```

### ADI..............................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The ADI parameter specifies the alternate delay interval in seconds for an alternate CICS region when you
are running CICS with XRF.
ADI={ 30 |number}
The minimum delay that you can specify is 5 seconds. This is the time that must elapse between the
(apparent) loss of the surveillance signal in the active CICS region, and any reaction by the alternate
CICS region. The corresponding parameter for the active is PDI. ADI and PDI need not have the same
value.
Note: You must give careful consideration to the values you specify for the parameters ADI and
JESDI so that they do not conflict with your installation's policy on PR/SM RESETTIME and the XCF
INTERVAL and OPNOTIFY intervals. You should ensure that the sum of the interval you specify for
ADI plus JESDI exceeds the interval specified by the XCF INTERVAL and the PR/SM policy interval
RESETTIME.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
```
Chapter 1. System initialization parameter summary   15
```

```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The XRF system initialization parameter
```
### AIBRIDGE...................................................................................................................................................

```
The AIBRIDGE parameter specifies whether the autoinstall user replaceable module (URM) is to be called
when CICS is creating bridge facilities (virtual terminals) used by the 3270 bridge mechanism. Specify this
parameter only in the bridge router region.
Bridge facility terminal names and netnames are normally allocated dynamically by the bridge
mechanism, but if the AIBRIDGE system initialization parameter is set to YES, the terminal autoinstall
control program is called and can be used to assign installation specific names.
AIBRIDGE={AUTO|YES}
Valid values are as follows:
AUTO
This is the default, and specifies that bridge facilities are defined automatically by CICS. The
autoinstall URM is not called.
YES
Specifies that the autoinstall URM is to be called for all new bridge facilities.
For information about writing an autoinstall user replaceable module, see Writing a program to control
autoinstall of programs.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Introduction to the 3270 bridge
How bridge facility virtual terminals are autoinstalled
Defining the bridge facility
```
### AICONS......................................................................................................................................................

```
The AICONS parameter specifies whether you want autoinstall support for consoles.
You can also set the state of autoinstall support for consoles dynamically using the SET AUTOINSTALL
command.
AICONS={NO|YES|AUTO}
Valid values for this parameter are as follows:
NO
This is the default, and specifies that the CICS regions does not support autoinstall for consoles.
YES
Specifies that console autoinstall is active and CICS is to call the autoinstall control program, as
part of the autoinstall process, when an undefined console issues a z/OS MODIFY command to
CICS.
AUTO
Specifies that console autoinstall is active but CICS is not to call the autoinstall control program
when an undefined console issues a z/OS MODIFY command to CICS. CICS is to autoinstall
undefined consoles automatically without any input from the autoinstall control program. The
4-character termid required for the console's TCT entry is generated by CICS, beginning with a ¬
(logical not) symbol.
```
**16**   CICS TS for z/OS: System Initialization Parameter Reference


### AIEXIT........................................................................................................................................................

```
The AIEXIT parameter specifies the name of the autoinstall user-replaceable program that you want
CICS to use when autoinstalling local z/OS Communications Server terminals, APPC connections, virtual
terminals, and shipped terminals and connections.
AIEXIT={DFHZATDX|DFHZATDY|name}
Autoinstall is the process of installing resource definitions automatically, using z/OS Communications
Server logon or BIND data, model definitions, and an autoinstall program.
You can specify only one user-replaceable program on the AIEXIT parameter. Which of the CICS-
supplied programs (or customized versions thereof) that you choose depends on what combination of
resources you need to autoinstall.
For background information about autoinstall, see Autoinstall. Valid values for this parameter are as
follows:
DFHZATDX
A CICS-supplied autoinstall user program. This value is the default. It installs definitions for:
```
- Locally-attached z/OS Communications Server terminals
- Virtual terminals used by the CICS Client products
- Remote shipped terminals
- Remote shipped connections
**DFHZATDY**
A CICS-supplied autoinstall user program. It installs definitions for:
- Locally-attached z/OS Communications Server terminals
- Local APPC connections
- Virtual terminals used by the CICS Client products
- Remote shipped terminals
- Remote shipped connections
**name**
The name of your own customized autoinstall program, which can be based on one of the supplied
sample programs. For programming information about writing your own autoinstall program, see
Writing a program to control autoinstall of terminals.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

### AILDELAY...................................................................................................................................................

```
The AILDELAY parameter specifies the delay period that elapses after all sessions between CICS and an
autoinstalled terminal, APPC device, or APPC system are ended, before the terminal or connection entry is
deleted.
AILDELAY={ 0 |hhmmss}
All sessions are ended when the terminal or system logs off, or when a transaction disconnects it from
CICS.
The AILDELAY parameter does not apply to the following types of autoinstalled APPC connection,
which are not deleted:
```
- Sync level 2-capable connections (for example, CICS-to-CICS connections)

```
Chapter 1. System initialization parameter summary   17
```

- Sync level 1-only, limited resource connections installed on a CICS that is a member of a generic
    resource group
Valid values for this parameter are as follows:
**0**
    The default is 0. For non-LU6.2 terminals and LU6.2 single-session connections installed by a
    CINIT, 0 means that the terminal entry is deleted as soon as the session is ended. For LU6.2
    connections installed by a BIND, 0 means that the connection is deleted as soon as all sessions
    are ended, but is reusable if a new BIND occurs before the deletion starts.
**hhmmss**
    A 1 to 6-digit number. If you leave out the leading zeros, they are supplied (for example, 123
    becomes 000123—that is, 1 minute 23 seconds).
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
**Related information**
Writing a program to control autoinstall of consoles
Autoinstalling z/OS consoles
Component reference: Autoinstall for terminals, consoles and APPC connections

### AIQMAX......................................................................................................................................................

```
The AIQMAX parameter specifies the maximum number of z/OS Communications Server terminals and
APPC connections that can be queued concurrently for autoinstall, the limit is the sum of installs and
deletes.
AIQMAX={ 100 |number}
The value for this parameter must be a number in the range 0 through 999. The default is 100. A zero
value disables the autoinstall function.
Specify a number that is large enough to allow for installs and deletes of both APPC connections and
terminals.
Note: This value does not limit the total number of terminals that can be autoinstalled. If you have a
large number of terminals autoinstalled, CICS shutdown can fail due to the MXT system initialization
parameter being reached or CICS becoming short on storage. For information about preventing this
possible cause of shutdown failure, see MVS and DASD: improving performance.
If you issue INQUIRE AUTOINSTALL , the MAXREQS value returned corresponds to the AIQMAX system
initialization parameter.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Autoinstall performance
Tuning automatic installation of terminals
Component reference: Autoinstall for terminals, consoles and APPC connections
INQUIRE AUTOINSTALL
```
**18**   CICS TS for z/OS: System Initialization Parameter Reference


### AIRDELAY...................................................................................................................................................

```
The AIRDELAY parameter specifies the delay period that elapses after an emergency restart before
autoinstalled terminal and APPC connection entries that are not in session are deleted.
AIRDELAY={ 700 |hhmmss}
The AIRDELAY parameter also applies when you issue a z/OS Communications Server CEMT SET
VTAM OPEN command after a z/OS Communications Server abend and PSTYPE=MNPS is coded. This
causes autoinstalled resources to be deleted, if the session was not restored and has not been used
since the ACB was opened.
The AIRDELAY parameter does not apply to the following types of autoinstalled APPC connection,
which are always written to the CICS global catalog and recovered during a warm or emergency start:
```
- Sync level 2-capable connections (for example, CICS-to-CICS connections)
- Sync level 1-capable, limited resource connections installed on a CICS that is a member of a generic
    resource group
**hhmmss**
    A 1-to 6-digit number. If you leave out the leading zeros, they are supplied. The default is 700,
    meaning a delay of 7 minutes. A value of 0 means that autoinstalled definitions are not written to
    the global catalog and therefore are not restored at an emergency restart.
    For guidance about the performance implications of setting different **AIRDELAY** values, see MVS
    and DASD: improving performance.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

### AKPFREQ....................................................................................................................................................

```
The AKPFREQ parameter specifies the number of write requests to the CICS system log stream output
buffer required before CICS writes an activity keypoint.
For information about activity keypointing, see The activity keypoint frequency (AKPFREQ).
AKPFREQ={ 4000 |number}
4000
This is the default. You are recommended to allow AKPFREQ to assume its default value.
number
number can be 0 (zero) or any value in the range 50 through 65535. You cannot specify a number
in the range 1 - 49.
```
**Effect of disabling activity keypointing**

```
If you specify AKPFREQ=0 , no activity keypoints are written, with the following consequences:
```
- The CICS system log automatic deletion mechanism does not work so efficiently in this situation. The
    average system log occupancy would merely increase, maybe dramatically for some users. Without
    efficient automatic deletion, the log stream spills on to auxiliary storage, and from there onto tertiary
    storage (unless you control the size of the log stream yourself).
- Emergency restarts are not prevented, but the absence of activity keypoints on the system log affects
    the performance of emergency restarts because CICS must read backwards through the entire log
    stream.
- Backout-while-open (BWO) support for non-RLS activities is seriously affected, because without activity
    keypointing, tie-up records are not written to the forward recovery logs and the data set recovery point

```
Chapter 1. System initialization parameter summary   19
```

```
is not updated. Therefore, for forward recovery to take place, all forward recovery logs must be kept
since the data set was first opened for update after the last image copy. If there are many inserts or
records that change length, a lot of forward recovery could be required. If, however, a record is just
updated and the length is unchanged, there is no CI split. For information about TURs and recovery
points, see Backup-while-open (BWO).
```
- Replication support is affected, because without activity keypointing, tie-up records are not written to
    replication logs. This can affect the performance of the replication engine.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

### APPLID.......................................................................................................................................................

```
The APPLID parameter specifies the z/OS Communications Server application identifier for this CICS
region.
APPLID={DBDCCICS| applid }
Valid values are as follows:
applid
This name, 1 through 8 characters, identifies the CICS region in the z/OS Communications
Server network. It must match the name field specified in the APPL statement of the z/OS
Communications Server VBUILD TYPE=APPL definition. For an example, see Defining specific
APPL definitions and APPL parameters to SNA.
If CICS is running in a sysplex, its APPLID must be unique in the sysplex.
This parameter can be used also as the application identifier of this CICS region on IPIC
connections.
When you define this CICS region to another CICS region, in an MRO or ISC over SNA
CONNECTION definition you specify the APPLID using the NETNAME attribute; in an IPIC IPCONN
definition you specify the APPLID using the APPLID attribute.
If the CICS region uses XRF, the form of the APPLID parameter is as follows:
APPLID=( generic_applid , specific_applid )
Specifies the generic and specific XRF APPLIDs for the CICS region. Both APPLIDs must be 1
through 8 characters long and the specific APPLID must be unique in the sysplex. If, on CICS
startup, the specified specific APPLID is found to duplicate the (specific or only) APPLID of any
other CICS region currently active in the sysplex, CICS issues message DFHPA1946 and fails to
initialize.
generic_applid
The generic APPLID for both the active and the alternate CICS regions. You must specify the
same name for generic_applid on the APPLID system initialization parameter for both CICS
regions. Because IRC uses the generic_applid to identify the CICS regions, there can be no IRC
connection for an alternate CICS region until takeover has occurred and the alternate CICS
region becomes the active CICS region.
When you define this XRF pair to another CICS region, in an MRO or ISC over SNA
CONNECTION definition you specify the generic APPLID using the NETNAME attribute; in an
IPIC IPCONN definition you specify the generic APPLID using the APPLID attribute.
Do not confuse the term generic applid with generic resource name. Generic APPLIDs
apply only to CICS regions that use XRF. Generic resource names apply only to z/OS
Communications Server generic resource groups.
```
**20**   CICS TS for z/OS: System Initialization Parameter Reference


```
specific_applid
Specifies the CICS region in the z/OS Communications Server network. It must match the label
specified in the z/OS Communications Server VBUILD TYPE=APPL definition. You must specify
a different specific_applid on the APPLID system initialization parameter for the active and for
the alternate CICS region. Also, generic_applid and specific_applid must be different.
The active and alternate CICS regions use the z/OS Communications Server MODIFY
USERVAR command to set a user application name variable, so users do not need to know
which CICS region is active at any instant.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### AUTCONN...................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The AUTCONN parameter specifies that the reconnection of terminals after an XRF takeover is to be
delayed, to allow time for manual switching.
AUTCONN={ 0 |hhmmss} (alternate)
The delay is hh hours, mm minutes, and ss seconds. The default value of zero means that there is no
delay in the attempted reconnection.
The interval specified is the delay before the CXRE transaction runs. CXRE tries to reacquire any
XRF-capable (class 1) terminal session that failed to get a backup session, or failed the switch for
some other reason. CXRE tries to reacquire other terminals that were in session at the time of the
takeover.
Note that the same delay interval applies to the connection of terminals with AUTOCONNECT(YES)
specified in the TYPETERM definition, at a warm or emergency restart, whether or not you have coded
XRF=YES.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The XRF system initialization parameter
```
### AUTODST....................................................................................................................................................

```
The AUTODST parameter specifies whether CICS is to activate automatic dynamic storage tuning for
application programs. This function, if used in a system with active, storage intensive programs, can save
CPU consumption by minimizing GETMAIN and FREEMAIN requests that would be otherwise needed.
AUTODST={NO|YES}
Valid values are as follows:
NO
Automatic dynamic storage tuning is not required and CICS does not request this support from
Language Environment®.
```
```
Chapter 1. System initialization parameter summary   21
```

#### YES

```
Automatic dynamic storage tuning is required. This is activated during CICS startup when
Language Environment is being initialized. CICS indicates that it can support dynamic storage
tuning to Language Environment, and if Language Environment responds by indicating that it also
supports the facility, CICS and Language Environment are synchronized to provide the required
support.
For more information, see the appropriate z/OS Language Environment information.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Tuning with Language Environment
AUTODST: Language Environment automatic storage tuning
```
### AUTORESETTIME.......................................................................................................................................

```
The AUTORESETTIME parameter specifies the action CICS takes for automatic time changes.
AUTORESETTIME={IMMEDIATE|NO|YES}
Valid values are as follows:
IMMEDIATE
CICS issues a PERFORM RESET command to synchronize the CICS time-of-day with the system
time-of-day if, at the next task attach, the CICS time-of-day differs from the system time-of-day.
CICS issues message DFHIC0801 when the times are synchronized.
NO
CICS issues message DFHAP1500 to indicate that a CEMT PERFORM RESET command is required
to synchronize the CICS time-of-day with the system time-of-day.
YES
CICS issues a PERFORM RESET command to synchronize the CICS time-of-day with the system
time-of-day if, at the next local midnight, the CICS time-of-day differs from the system time-of-
day by more than 30 minutes. For example, setting clocks forward or back to adjust for summer
and winter time. CICS issues message DFHIC0801 when the times are synchronized.
Note: Setting clocks back might cause end-of-day statistics to be written twice.
Recommendation: To ensure that the correct local time is used by all CICS functions, use the CEMT
PERFORM RESET command immediately whenever you alter the system date or the time-of-day in
the z/OS TOD clock while a CICS region is running.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Effect of daylight saving time changes
```
**22**   CICS TS for z/OS: System Initialization Parameter Reference


### AUXTR........................................................................................................................................................

```
The AUXTR parameter specifies whether the auxiliary trace destination is to be activated at system
initialization.
This parameter controls whether any of the three types of CICS trace entry are written to the auxiliary
trace data set. The three types are:
```
- CICS system trace (see the **SYSTR** parameter)
- User trace (see the **USERTR** parameter)
- Exception trace (which are always made and are not controlled by a system initialization parameter)
When CICS is running, you can change auxiliary trace settings dynamically through the CETR transaction.
**AUXTR={OFF|ON}**
    Valid values are as follows:
    **OFF**
       Do not activate auxiliary trace.
    **ON**
       Activate auxiliary trace.
**Related concepts**
CICS auxiliary trace and auxiliary trace data sets
**Related tasks**
Setting trace flags and trace destinations when CICS is running
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The AUXTRSW system initialization parameter
The **AUXTRSW** parameter specifies whether you want the auxiliary trace autoswitch facility.
The INTTR system initialization parameter
The **INTTR** system initialization parameter specifies whether the internal CICS trace destination is to be
activated at system initialization.
Trace utility print program (DFHTUnnn)

### AUXTRSW...................................................................................................................................................

```
The AUXTRSW parameter specifies whether you want the auxiliary trace autoswitch facility.
Two auxiliary trace data sets, DFHAUXT and DFHBUXT, are available to collect trace data when you use
CICS auxiliary trace. You can choose to use only one data set or both data sets. When you use both data
sets, you can use the AUXTRSW parameter to specify the action to take when one data set is full. When
CICS is running, you can also change the setting through the CETR transaction.
AUXTRSW={NO|NEXT|ALL}
Valid values are as follows:
NO
Disables the autoswitch facility.
NEXT
Enables the autoswitch facility to switch to the next data set at end of file of the first data set used
for auxiliary trace. Coding NEXT permits one switch only, and when the second data set is full,
auxiliary trace is switched off.
```
```
Chapter 1. System initialization parameter summary   23
```

#### ALL

```
Enables the autoswitch facility to switch to the inactive data set at every end of file. Coding ALL
permits continuous switching between the two auxiliary trace data sets, DFHAUXT and DFHBUXT,
and whenever a data set is full, it is closed and the other data set is opened.
Related concepts
CICS auxiliary trace and auxiliary trace data sets
Related tasks
Setting up auxiliary trace data sets
Setting trace flags and trace destinations when CICS is running
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The AUXTR system initialization parameter
The AUXTR parameter specifies whether the auxiliary trace destination is to be activated at system
initialization.
Trace utility print program (DFHTUnnn)
```
### BMS............................................................................................................................................................

```
The BMS system initialization parameter specifies which version of basic mapping support you require in
CICS.
BMS=({MINIMUM|STANDARD|FULL }[,COLD][,{UNALIGN |ALIGN}] [,{ DDS|NODDS}])
The function included in each version of BMS is shown in BMS support levels. The parameter BMS can
be overridden during CICS initialization.
MINIMUM
The minimum version of BMS is included.
STANDARD
The standard version of BMS is included.
FULL
The full version of BMS is included. This value is the default.
COLD
CICS deletes delayed messages from temporary storage, and destroys their interval control
elements (ICEs). COLD forces the deletion of messages regardless of the value in effect for START.
If COLD is not specified, the availability of messages depend on the values in effect for the START
and TS parameters.
UNALIGN
Specifies that all BMS maps assembled before CICS/OS/VS Version 1 Release 6 are unaligned.
Results are unpredictable if the stated alignment does not match the actual alignment.
ALIGN
All BMS maps assembled before CICS/OS/VS Version 1 Release 6 are aligned.
DDS
BMS is to load suffixed versions of map sets and partition sets. BMS first tries to load a version
that has the alternate suffix (if the transaction uses the alternate screen size). If the load fails,
BMS tries to load a version that has the default map suffix. If this fails too, BMS tries to load the
unsuffixed version. DDS, which stands for "device dependent suffixing", is the default.
You need to use map suffixes only if the same transaction is to be run on terminals with different
characteristics (in particular, different screen sizes). If you do not use suffixed versions of map
sets and partition sets, CICS need not test for them.
```
**24**   CICS TS for z/OS: System Initialization Parameter Reference


#### NODDS

```
BMS is not to load suffixed versions of map sets and partition sets. Specifying NODDS avoids the
search for suffixed versions, saving processor time.
```
```
Table 2. Versions of BMS
```
```
BMS version Devices supported Function provided
```
```
MINIMUM All 3270 system display units and
printers except SNA character
string printers, which are defined
as DEVICE(SCSPRINT) on the
RDO TYPETERM definition or as
TRMTYPE=SCSPRT in DFHTCT
```
```
SEND MAP command, RECEIVE
MAP command, SEND CONTROL
command. Default and alternate
screens; extended attributes;
map set suffixes; screen
coordination with null maps; and
block data
```
```
STANDARD All devices supported by BMS.
These are listed in BMS support
levels
```
```
All function of MINIMUM, as well
as outboard formats, partitions,
controlling a magnetic slot
reader, NLEOM mode for 3270
system printers, SEND TEXT
command, and Subsystem LDC
controls.
```
```
FULL All devices supported by BMS.
These are listed in BMS support
levels
```
```
Same as STANDARD, as
well as terminal operator
paging, cumulative mapping,
page overflow, cumulative
text processing, routing,
message switching returning
BMS-generated data stream to
program before output.
```
```
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### BRMAXKEEPTIME......................................................................................................................................

```
The BRMAXKEEPTIME parameter specifies the maximum time (in seconds) that bridge facilities (virtual
terminals used by the 3270 bridge) are kept if they are not used.
BRMAXKEEPTIME={ 86400 |number}
The client application can specify this timeout value when it sends a request to run a transaction using
the Link3270 bridge. If the client specifies a larger value than the BRMAXKEEPTIME value in the AOR,
then CICS will change this parameter in the link parameter list.
number
The maximum timeout value that a client can specify (in seconds), before an unused bridge
facility is deleted. The value specified must be in the range 0 to 86400. A value of 0 means that
bridge facilities are never kept at the end of a transaction; therefore, CICS will not be able to
run pseudoconversational transactions. This may be useful if the region is only used for inquiry
transactions. The default value is 24 hours (86400 seconds).
Related reference
“System initialization parameter summary” on page 1
```
```
Chapter 1. System initialization parameter summary   25
```

```
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
The bridge facility
The Link3270 bridge mechanism
Using the Link3270 bridge
```
### CDSASZE....................................................................................................................................................

```
The CDSASZE system initialization parameter specifies the size of the CDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
CDSASZE={0K|number}
Valid values are as follows:
0 (zero)
The size of the CDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the CDSA dynamic storage area is fixed. Specify number
as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes (256 KB).
If the value you specify is not a multiple of 256 KB, CICS rounds up the value to the next multiple.
You can specify number as a number of bytes, a whole number of kilobytes, or a whole number of
megabytes. Use the letter M to indicate that the value represents a whole number of megabytes
(for example, 4 M). Use the letter K to indicate that the value represents a whole number of
kilobytes (for example, 4096 K), in which case the number is rounded up to the number of
megabytes.
Restriction: You can specify the CDSASZE parameter in PARM, SYSIN, or CONSOLE only.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### CERTEXPIRYWARN....................................................................................................................................

```
6.2
Applies to 6.2.
The CERTEXPIRYWARN parameter specifies whether CICS warns about expiring certificates, and if so, how
many days ahead of the expiry.
Set CERTEXPIRYWARN in web owning regions to check certificates in the certificate chain, such as client
certificates, external server certificates, and signing certificates.
Note:
CERTEXPIRYWARN checks only certificates that are sent by the partner system through TLS connections.
To check expiring certificates that are managed by CICS, that is, those defined in RACF®, use the
RACF_CERTIFICATE_EXPIRATION check provided by IBM Health Checker for z/OS instead.
```
**26**   CICS TS for z/OS: System Initialization Parameter Reference


```
CERTEXPIRYWARN={NO| expiry_days }
NO
Disables checking for certificate expiry.
This value is the default because there is a small cost of checking all certificates.
expiry_days
Specifies a value in days, in the range of 1–999. CICS issues a warning message DFHSO1100I
if any certificates are about to expire within the specified days. The message provides details
about the expiring certificate. CICS also issues a trace entry (trace point ID is SO 0863) if the SO
trace level is set to 2. CICS generates the warning message and the trace only once per day per
certificate.
To enable certificate expiry warning, that is, setting CERTEXPIRYWARN to a positive integer, you
must use z/OS 2.5 with APAR OA64071, or a later version of z/OS.
If you also use the RACF_CERTIFICATE_EXPIRATION check to warn about RACF defined
certificates, you can set CERTEXPIRYWARN to the same value in days as what is specified on
that check to match.
There is a small impact on performance when CERTEXPIRYWARN is in use.
Related topic
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Performance report
```
### CHKSTRM...................................................................................................................................................

```
The CHKSTRM parameter specifies that terminal storage-violation checking is to be activated or
deactivated. CICS can detect storage violations when the duplicate storage accounting area (SAA) or
the initial SAA of a TIOA storage element has become corrupted (that is, the two storage check zones of
the duplicate SAA and the initial SAA are not identical).
CHKSTRM={CURRENT|NONE}
Valid values are as follows:
CURRENT
TIOA storage violations are to be checked.
NONE
TIOA storage-violation checking is to be deactivated.
You can also use the CICS-supplied transaction, CSFE, to switch terminal storage-violation checking on
and off.
For information about checking for storage violations, see Dealing with storage violations.
Restriction: You can specify the CHKSTRM parameter in PARM, SYSIN, or CONSOLE only.
Related concepts
How you can protect CICS storage
Reducing storage violations
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
```
Chapter 1. System initialization parameter summary   27
```

```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSFE - terminal and system test
```
### CHKSTSK....................................................................................................................................................

```
The CHKSTSK parameter specifies that task storage-violation checking at startup is to be activated or
deactivated. CICS can detect storage violations when the leading storage check zone or the trailing
storage check zone of a user task storage element has become corrupted.
CHKSTSK={CURRENT|NONE}
Valid values are as follows:
CURRENT
All storage areas on the transaction storage chain for the current task only are to be checked.
NONE
Task storage-violation checking is to be deactivated.
You can also use the CICS-supplied transaction, CSFE, to switch task storage-violation checking on and
off.
For information about checking for storage violations, see Dealing with storage violations.
Restriction: You can specify the CHKSTSK parameter in PARM, SYSIN, or CONSOLE only.
Related concepts
How you can protect CICS storage
Reducing storage violations
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSFE - terminal and system test
```
### CICSSVC.....................................................................................................................................................

```
The CICSSVC parameter specifies the number that you have assigned to the CICS type 3 SVC. If you use a
non-default SVC number, you must define it to CICS on the CICSSVC system initialization parameter.
CICSSVC={ 216 |number}
The default number is 216. A CICS type 3 SVC with the specified or default number must be installed
in the LPA. For information about installing the CICS SVC, see Installing the CICS SVCs.
CICS checks if the SVC number supplied corresponds to the correct level of the CICS Type 3
SVC module, DFHCSVC. If the SVC number does not correspond to the correct level of DFHCSVC,
the following can happen, depending on the value specified for the PARMERR system initialization
parameter:
```
- CICS is terminated with a system dump.
- The operator is allowed to retry using a different SVC number.
For details of the **PARMERR** system initialization parameter, see PARMERR.
**Note:** If IBM changes the Type 3 SVC, for example at a new release or because of a service update, you
must reinstall the current level of the CICS Type 3 SVC into the link pack area (LPA) and perform an IPL
with the CLPA option.
**Related reference**
“System initialization parameter summary” on page 1

**28**   CICS TS for z/OS: System Initialization Parameter Reference


```
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### CILOCK.......................................................................................................................................................

```
The CILOCK system initialization parameter specifies whether or not the control interval lock of a non-RLS
VSAM file is to be kept after a successful read-for-update request.
CILOCK={NO|YES}
Valid values are as follows:
NO
This is the default and specifies that the control interval is to be freed. This allows other tasks to
access other records in the same control interval, without an exclusive control conflict occurring.
In these cases throughput should be greater. Note that the record lock on the record for which
the read-for-update was first issued, still prevents other tasks from updating this record, even
though the control interval lock has been released. When the record is rewritten or deleted, the
read-for-update is reissued to VSAM as part of the update processing.
If a WRITE is issued by another task during a READ UDPATE, the WRITE receives a DUPREC
condition.
YES
This specifies that the control interval is not to be freed. This means that a subsequent rewrite or
delete request does not need to reissue the read-for-update request to VSAM. However, if other
tasks attempt to access other records in the same control interval, an exclusive control conflict
occurs on this control interval, forcing these tasks to wait until the update request completes.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
VSAM data sets
VSAM and file control: improving performance
```
### CLINTCP.....................................................................................................................................................

```
The CLINTCP parameter specifies the default client code page to be used by the DFHCNV data conversion
table, but only if the CLINTCP parameter in the DFHCNV macro is set to SYSDEF.
CLINTCP={ 437 |code page}
The code page is a field of up to 8 characters and can take the values supported by the CLINTCP
parameter in the DFHCNV macro. For the list of valid code pages, see CICS-supported conversions.
The default is 437.
You define the conversion table with DFHCNV resource definition macros. The output of the DFHCNV
macro assembly contains templates specifying resource conversion requirements and conversion tables
to enable the required conversions. User-generated conversion tables must be placed in the DFHCNV
macro source. For details, see Defining the conversion table.
To learn about how data conversion works in CICS, see The conversion process.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
```
Chapter 1. System initialization parameter summary   29
```

```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The SRVERCP system initialization parameter
The SRVERCP system initialization parameter specifies the default server code page to be used by the
DFHCNV data conversion table but only if the SRVERCP parameter in the DFHCNV macro is set to SYSDEF.
CICS-supported conversions
```
### CLSDSTP.....................................................................................................................................................

```
The CLSDSTP system initialization parameter specifies the notification required for an EXEC CICS
ISSUE PASS command.
CLSDSTP={NOTIFY|NONOTIFY}
This parameter is applicable to both autoinstalled and non-autoinstalled terminals. You can use
the notification in a user-written node error program to reestablish the CICS session when a z/OS
Communications Server VTAM CLSDST PASS request resulting from an EXEC CICS ISSUE PASS
command fails. For more information about the EXEC CICS ISSUE PASS command, see ISSUE
PASS.
NOTIFY
CICS requests notification from z/OS Communications Server when the EXEC CICS ISSUE PASS
command is executed.
NONOTIFY
CICS does not request notification from z/OS Communications Server.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Writing a node error program
```
### CLT..............................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The command list table is used by XRF and contains a list of z/OS system commands and messages to the
operator, to be issued during takeover. The CLT parameter specifies the suffix for the command list table
(CLT), if this SIT is used by an alternate XRF system.
CLT=xx (alternate)
The name of the table is DFHCLTxx. For information about coding the macros for this table, see
Command list table (CLT).
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The XRF system initialization parameter
```
**30**   CICS TS for z/OS: System Initialization Parameter Reference


### CMDPROT...................................................................................................................................................

```
The CMDPROT parameter specifies whether to allow or inhibit CICS validation of start addresses of storage
referenced as output parameters on EXEC CICS commands.
CMDPROT={YES|NO}
Valid values are as follows:
YES
CICS validates the initial byte at the start of any storage that is referenced as an output parameter
on EXEC CICS commands to ensure that the application program has write access to the storage.
This ensures that CICS does not overwrite storage on behalf of the application program when the
program itself cannot do so. If CICS detects that an application program has asked CICS to write
into an area to which the application does not have addressability, CICS abends the task with an
AEYD abend.
The level of protection against bad addresses depends on the level of storage protection in the
CICS environment. The various levels of protection provided when you specify CMDPROT=YES are
shown in Table 3 on page 31.
NO
CICS does not perform any validation of addresses of the storage referenced by EXEC CICS
commands. This means that an application program could cause CICS to overwrite storage to
which the application program itself does not have write access.
For information about DSAs, see CICS dynamic storage areas (DSAs).
```
```
Table 3. Levels of protection provided by CICS validation of application-supplied addresses
```
```
Environment Execution key of affected
programs
```
```
Types of storage referenced by
applications that cause AEYD
abends
```
```
Read-only storage
(RENTPGM=PROTECT)
```
```
CICS-key and user-key CICS key 0 read-only storage
```
```
Subsystem storage protection
(STGPROT=YES)
```
```
User-key All CICS-key storage
```
```
Transaction isolation
(TRANISO=YES)
```
```
User-key and ISOLATE(YES) Task-lifetime storage of all other
transactions
```
```
Transaction isolation
(TRANISO=YES)
```
```
User-key and ISOLATE(NO) Task-lifetime storage of all
except other user key and
ISOLATE(NO) transactions
```
```
Base CICS (all storage
is CICS key 8 storage)
(RENTPGM=NOPROTECT;
STGPROT=NO; and
TRANISO=NO)
```
```
CICS-key and user-key MVS™ storage only
```
```
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
```
Chapter 1. System initialization parameter summary   31
```

```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### CMDSEC......................................................................................................................................................

```
The CMDSEC parameter specifies whether or not you want CICS to honor the CMDSEC option specified on
a transaction's resource definition.
CMDSEC={ASIS|ALWAYS}
Valid values are as follows:
ASIS
CICS honors the CMDSEC option defined in a transaction's resource definition. CICS calls its
command security checking routine only when CMDSEC(YES) is specified in a transaction resource
definition.
ALWAYS
CICS overrides the CMDSEC option, and always calls its command security checking routine to
issue the appropriate call to the SAF interface.
Note:
```
1. Specify ALWAYS when you want to control the use of the SPI in all your transactions. Be aware
    that this might incur additional overhead. The additional overhead is caused by CICS issuing
    the command security calls on every eligible **EXEC CICS** command, which are _all_ the system
    programming interface (SPI) commands.
2. If you specify ALWAYS, command checking applies to CICS-supplied category 2 transactions.
    You must authorize all users of these transactions to use any SPI commands that these
    transactions use; otherwise, you will get abends due to security failures. CICS-supplied
    category 3 transactions do not use SPI commands; therefore, the default user ID does not
    need to be authorized for SPI commands.
**Restriction:** You can specify the CMDSEC parameter in the SIT, PARM, or SYSIN only.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
**Related information**
Command security

### CONFDATA..................................................................................................................................................

```
The CONFDATA parameter specifies whether CICS is to redact sensitive data that might otherwise appear
in CICS trace entries or in dumps.
CONFDATA={HIDE|SHOW}
HIDE
CICS is to redact user sensitive data from CICS trace entries. The action taken by CICS is subject
to the individual CONFDATA attribute on the transaction resource definition.
SHOW
Data redaction is not in effect. User data is traced regardless of the CONFDATA option specified
in transaction resource definitions. This option overrides the CONFDATA option in transaction
resource definitions.
The CONFDATA system initialization parameter should usually be set to the default value of HIDE to avoid
passwords in transport data accidentally being exposed in trace entries or dumps. Most problems can be
```
**32**   CICS TS for z/OS: System Initialization Parameter Reference


```
diagnosed without this data. If it is necessary to reproduce problems with CONFDATA set to SHOW, be
aware that password data could be exposed.
See Removing sensitive data from CICS trace using CONFDATA for details of the CONFDATA mechanism
including the interaction between the CONFDATA system initialization parameter and the CONFDATA
transaction attribute.
You cannot modify the CONFDATA system initialization parameter while CICS is running. You must restart
CICS to apply a change.
Restriction: You can specify the CONFDATA parameter in the SIT, PARM, and SYSIN only.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### CONFTXT....................................................................................................................................................

```
The CONFTXT system initialization parameter specifies whether CICS is to prevent z/OS Communications
Server from tracing user data.
CONFTXT={NO|YES}
Valid values are as follows:
NO
CICS does not prevent z/OS Communications Server from tracing user data.
YES
CICS prevents z/OS Communications Server from tracing user data.
Restriction: You can specify the CONFTXT parameter in the SIT, PARM, and SYSIN only.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Using z/OS Communications Server SNA exit trace
Using z/OS Communications Server SNA buffer trace
```
### CPSMCONN................................................................................................................................................

```
The CPSMCONN parameter specifies whether you want CICS to invoke the specified CICSPlex® SM
component during initialization of the region.
Using the CPSMCONN parameter causes the CICSPlex SM component to start during the PLT phase of CICS
initialization. This means that MASPLTWAIT and other PLT-related CICSPlex SM parameters are still valid
and should be specified as necessary. To understand which user ID the CICSPlex SM agents run under,
see Determining the CICSPlex SM agent user ID.
CPSMCONN={NO|CMAS|LMAS|SMSSJ|WUI}
You can initialize the region as one of the following:
```
- A CICSPlex SM address space (CMAS)
- A CICSPlex SM local managed application system (MAS)
- A CICSPlex SM Web User Interface (WUI) server

```
Chapter 1. System initialization parameter summary   33
```

- A CICS System Management Single Server (SMSS)
**NO**
    Do not invoke any CICSPlex SM initialization code in this region.
**CMAS**
    Invoke CICSPlex SM code automatically during CICS initialization to initialize the region as a
    CMAS. The other information CICSPlex SM needs for a CMAS is taken from the CMAS parameters
    read from the EYUPARM data set.
    **Note:** If you specify **CPSMCONN** =CMAS, ensure that your CICS region startup JCL EXEC statement
    specifies the name of the CICSPlex SM CMAS program, EYU9XECS. For example:

```
//CMAS EXEC PGM=EYU9XECS,...,...
```
```
LMAS
Invoke CICSPlex SM code automatically during CICS initialization to initialize the region as a local
MAS. The other information CICSPlex SM needs for a MAS is taken from the MAS parameters read
from the EYUPARM data set.
SMSSJ
Initialize a single CICS region that is not part of a CICSplex as a CICS System Management Single
Server (SMSS) and automatically create a Liberty JVM server named EYUCMCIJ as the CMCI JVM
server of the region. For more information, see Setting up CMCI in a single CICS region.
WUI
Invoke CICSPlex SM code automatically during CICS initialization to initialize the region as a
CICSPlex SM WUI server. The other information CICSPlex SM needs is taken from the MAS and
WUI parameters read from the EYUPARM and EYUWUI data sets respectively.
For information about starting CICSPlex SM address spaces, see Installing CICS TS.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
### CRLPROFILE...............................................................................................................................................

```
The CRLPROFILE parameter specifies the name of the profile that is used to authorize CICS to access the
certification revocation lists (CRLs) that are stored in an LDAP server.
CRLPROFILE= PROFILENAME
The profile name is specified in the RACF LDAPBIND general resource class that contains bind
information for an LDAP server. The profile name must be uppercase and can be up to 246 characters
in length.
The profile must contain the name of the LDAP server and the distinguished name and password of
a user who is authorized to extract certification revocation lists from it. For more information about
setting up the profile, see Configuring LDAP for CICS use.
Specifying this parameter means that CICS checks each client certificate during the SSL negotiation
for a revoked status using the certificate revocation lists in the LDAP server. If the certificate is
revoked, CICS closes the connection immediately. If the CRLPROFILE parameter is omitted, CICS
does not check the revoked status of certificates during SSL handshakes.
If the CRLPROFILE parameter is specified but is invalid, or if the specified profile contains invalid
data, or if the LDAP server identified by the profile is unavailable when the CICS region starts, the
CICS region disables its own access to the LDAP server and does not check the revoked status of
certificates during SSL handshakes. Messages DFHSO0128 and DFHSO0129 report this problem. To
restore access, you must fix the error and restart the CICS region.
```
**34**   CICS TS for z/OS: System Initialization Parameter Reference


```
The bind information for the LDAP server is cached in the SSL environment for the CICS region,
which is managed by z/OS System SSL. When you issue the PERFORM SSL REBUILD command, the
bind information for the LDAP server is refreshed from RACF. The PERFORM SSL REBUILD command
cannot restore access to the LDAP server if the CICS region has disabled it. The refresh only takes
place for an LDAP server that was available to the CICS region at the time when the command was
issued.
```
### CSDACC......................................................................................................................................................

```
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
CSDACC={READWRITE|READONLY}
This parameter is effective only when you start CICS with a START=COLD parameter. If you code
START=AUTO and CICS performs a warm or emergency restart, the file resource definitions for the
CSD are recovered from the CICS global catalog. However, you can redefine the type of access
permitted to the CSD dynamically with a CEMT SET FILE or EXEC CICS SET FILE command.
READWRITE
Read/write access is allowed, permitting the full range of CEDA, CEDB, and CEDC functions to be
used.
READONLY
Read access only is allowed, limiting the CEDA and CEDB transactions to only those functions that
do not require write access.
Related tasks
Setting up the CICS system definition data set
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
SET FILE
CEMT SET FILE
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
```
```
Chapter 1. System initialization parameter summary   35
```

```
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDBKUP...................................................................................................................................................

```
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The BWO facility allows you to take a backup copy of a VSAM data set while it remains open for update.
Using BWO, only the updates that have been made since the last backup copy was taken need to be
recovered. This could considerably reduce the amount of forward recovery that is needed. If you want to
use BWO for the CSD, specify CSDBKUP=DYNAMIC.
The CSDBKUP , CSDRECOV , and CSDFRLOG system initialization parameters interact according to how they
are specified. For information about their effects when the SIT is assembled and during CICS override
processing, see Planning for backup and recovery.
CSDBKUP={STATIC|DYNAMIC}
STATIC
All CICS files open for update against the CSD data set must be quiesced before a DFHSM and
DFDSS backup of the CSD data set. The files must remain quiesced during the backup.
DYNAMIC
DFHSM and DFDSS are allowed to make a data set back up copy while CICS is updating the CSD.
Note that CSDBKUP=DYNAMIC is valid only if you have also specified CSDRECOV=ALL.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Backup-while-open (BWO)
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
```
**36**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDBUFND.................................................................................................................................................

```
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
CSDBUFND= number
The minimum you should specify is the number of strings coded on the CSDSTRNO parameter
plus 1, up to a maximum of 32768. Note that this parameter is used only if you have also coded
CSDLSRNO=NONE ; if you have coded CSDLSRNO=number , CSDBUFND is set to a value of 0 and
ignored.
If you specify a value for CSDBUFND that is less than the required minimum (the CSDSTRNO value
plus 1), VSAM automatically changes the number of buffers to the number of strings plus 1 when CICS
issues the OPEN macro for the CSD.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
Related tasks
Setting up the CICS system definition data set
Related reference
“System initialization parameter summary” on page 1
```
```
Chapter 1. System initialization parameter summary   37
```

```
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDBUFNI..................................................................................................................................................

```
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
CSDBUFNI= number
The minimum you should specify is the number of strings coded on the CSDSTRNO parameter, up to a
maximum of 32768. This parameter is used only if you have also coded CSDLSRNO=NONE ; if you have
coded CSDLSRNO=number , CSDBUFNI is set to a value of 0 and ignored.
```
**38**   CICS TS for z/OS: System Initialization Parameter Reference


```
If you specify a value for CSDBUFNI that is less than the required minimum (the CSDSTRNO value),
VSAM automatically changes the number of buffers to the number of strings when CICS issues the
OPEN macro for the CSD.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
```
**Related tasks**

Setting up the CICS system definition data set

**Related reference**

“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

**CSD-related system initialization parameters**

The CSDACC system initialization parameter
The **CSDACC** system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.

The CSDBKUP system initialization parameter
The **CSDBKUP** system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.

The CSDBUFND system initialization parameter
The **CSDBUFND** system initialization parameter specifies the number of buffers to be used for CSD data.

The CSDBUFNI system initialization parameter
The **CSDBUFNI** system initialization parameter specifies the number of buffers to be used for the CSD
index.

The CSDDISP system initialization parameter
The **CSDDISP** system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.

The CSDDSN system initialization parameter
The **CSDDSN** system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.

The CSDFRLOG system initialization parameter
The **CSDFRLOG** system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.

The CSDINTEG system initialization parameter
The **CSDINTEG** system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.

The CSDJID system initialization parameter
The **CSDJID** system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.

The CSDLSRNO system initialization parameter
The **CSDLSRNO** system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.

The CSDRECOV system initialization parameter
The **CSDRECOV** system initialization parameter specifies whether the CSD is a recoverable file.

The CSDRLS system initialization parameter
The **CSDRLS** system initialization parameter specifies whether CICS is to access the CSD in RLS mode.

The CSDSTRNO system initialization parameter

```
Chapter 1. System initialization parameter summary   39
```

```
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDDISP.....................................................................................................................................................

```
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
CSDDISP={OLD|SHR}
If no JCL statement for the CSD exists when it is opened, the open is preceded by a dynamic
allocation of the CSD using this disposition. If a DD statement exists in the JCL of the CICS startup job,
it takes precedence over this disposition.
OLD
The disposition of the CSD is set to OLD if dynamic allocation is performed.
SHR
The disposition of the CSD is set to SHR if dynamic allocation is performed.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
Related tasks
Setting up the CICS system definition data set
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
```
**40**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDDSN......................................................................................................................................................

```
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
CSDDSN= name
If no JCL statement exists for the CSD when it is opened, the open is preceded by a dynamic
allocation of the CSD using this DSNAME. If a DD statement exists in the JCL of the CICS startup job, it
takes precedence over this DSNAME.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
Related tasks
Setting up the CICS system definition data set
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
```
```
Chapter 1. System initialization parameter summary   41
```

```
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDFRLOG..................................................................................................................................................

```
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
CSDFRLOG=number
This parameter is meaningful only if CSDRECOV=ALL and CSDRLS=NO are specified, otherwise
it is ignored. If you specify CSDRLS=NO and CSDRECOV=ALL, but omit CSDFRLOG (or specify
CSDFRLOG=NO), the SIT assembly fails. However, if you specify an invalid combination as SIT
overrides, CICS initialization will fail.
CSDBKUP , CSDRECOV and CSDFRLOG are ignored if CSDRLS=YES is specified. This is because recovery
attributes (that is, the recoverability, the forward recovery LSN, and the BWO eligibility) must be
specified in the ICF catalog for data sets that are opened in RLS mode.
The recovery attributes can also be specified (optionally) in the ICF catalog when you specify
CSDRLS=NO. If you specify recovery attributes in both the ICF catalog and as system initialization
parameters, the ICF catalog values are used (but see the next paragraph).
For a CSD opened in a non-RLS mode (CSDRLS=NO), the CSDBKUP , CSDRECOV and CSDFRLOG system
initialization parameters interact according to how they are specified. For information about their
effects when the SIT is assembled and during CICS override processing, see Planning for backup and
recovery.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
number
The journal number that identifies the user journal that CICS is to use for forward recovery of the
CSD. CICS journal names are of the form DFHJ nn where nn is a number in the range 1 through 99.
CICS maps the resulting journal name (DFHJ01—DFHJ99) to a z/OS log stream.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
**42**   CICS TS for z/OS: System Initialization Parameter Reference


```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDINTEG..................................................................................................................................................

```
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
CSDINTEG={UNCOMMITTED|CONSISTENT|REPEATABLE}
If the CSD is not accessed in RLS mode (CSDRLS=NO), a value for CSDINTEG of CONSISTENT or
REPEATABLE will be changed to UNCOMMITTED.
UNCOMMITTED
The CSD is read without read integrity. For each read request, CICS obtains the current value
of the record as known to VSAM. No attempt is made to serialize this read request with any
concurrent update activity for the same record. The record returned may be a version updated
```
```
Chapter 1. System initialization parameter summary   43
```

```
by another RDO task but not yet committed, and this record could change if the update is
subsequently backed out.
CONSISTENT
CICS reads the CSD with consistent read integrity. If a record is being modified by another RDO
task, the READ request waits until the update is complete, the timing of which depends on
whether the CSD is recoverable or non-recoverable:
```
- For a recoverable CSD, the READ request completes when the updating transaction completes
    its next syncpoint or rollback.
- For a non-recoverable CSD, the READ completes as soon as the VSAM request performing the
    update completes.
**REPEATABLE**
CICS reads the CSD with repeatable read integrity. If the record is being modified by another
RDO task, the READ request waits until the update is complete, the timing of which depends on
whether the CSD is recoverable or non-recoverable:
- For a recoverable CSD, the READ request completes when the updating transaction completes
its next syncpoint or rollback.
- For a non-recoverable CSD, the READ completes as soon as the VSAM request performing the
update completes.
After the CSD read completes, a shared lock remains held until syncpoint. This guarantees that a
CSD record read within an RDO task cannot be modified until the end of the task (for example, a
CEDA transaction) that is reading the CSD.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
**CSD-related system initialization parameters**
The CSDACC system initialization parameter
The **CSDACC** system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The **CSDBKUP** system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The **CSDBUFND** system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The **CSDBUFNI** system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The **CSDDISP** system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The **CSDDSN** system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The **CSDFRLOG** system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter

**44**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDJID.......................................................................................................................................................

```
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
CSDJID={NO|number}
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
NO
You do not want automatic journaling for the CSD. This is the default.
number
A number in the range 1 through 99 to identify the journal that CICS is to use for automatic
journaling for the CSD. Mapping to a log stream works in the same way that CSDFRLOG does, that
is, nn maps to DFHJnn. 01 no longer maps to the system log.
The automatic journaling options enforced for the CSD when you code CSDJID=number
are JNLADD=BEFORE and JNLUPDATE=YES. These options are sufficient to record enough
information for a user-written forward recovery utility. No other automatic journaling options are
available for the CSD. For information about the options JNLADD=BEFORE and JNLUPDATE=YES,
see FILE resources.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
```
```
Chapter 1. System initialization parameter summary   45
```

```
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDLSRNO.................................................................................................................................................

```
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
CSDLSRNO={ 1 |number|NONE|NO}
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog. However, you can redefine the
LSR pool attribute for the CSD dynamically with an EXEC CICS SET FILE command.
1
The default LSR pool number is 1.
number
The number of the LSR pool the CSD is to be associated with. The number of the pool must be in
the range 1 through 255.
NONE|NO
The CSD is not to be associated with a local shared resource pool.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
```
**46**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDRECOV.................................................................................................................................................

```
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
CSDRECOV={NONE|ALL|BACKOUTONLY}
The CSDBKUP , CSDRECOV , and CSDFRLOG system initialization parameters interact according to how
they are specified, if CSDRLS=NO is specified. If CSDRLS=YES is specified, these parameters are
ignored, because the recovery attributes must be specified in the VSAM catalog (using the BWO, LOG,
and LOGSTREAMID parameters on DEFINE CLUSTER or ALTER CLUSTER). If CSDRLS=NO is specified
but LOG has been specified in the VSAM catalog, the recovery attributes are taken from the VSAM
catalog, and CSDBKUP, CSDRECOV, and CSDFRLOG do not need to be specified. If they are specified,
however, the rules given in Planning for backup and recovery must still be followed.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog.
NONE
The CSD is not recoverable.
```
```
Chapter 1. System initialization parameter summary   47
```

#### ALL

```
You want both forward recovery and backout for the CSD. If you code ALL, also specify CSDFRLOG
with the journal identification of the journal to be used for forward recovery of the CSD.
Note: If the journal you specify for logstreams associated with CSD recovery (CSDJID, CSDFRLOG,
and possibly the log of logs, DFGLGLOG) is a DASD-only log stream, there can be delays when you
use the CEDA transaction if the log stream requires a new connection. This delay is because the
z/OS System Logger is formatting the staging data set. Symptoms of the problem are:
DFHLG0771 07/08/01 03:30:42 IYOT1 A temporary error condition occurred
during MVS logger operation IXGWRITE for logstream xxxxxx.yyyyyy.zzzzzz.
MVS logger codes: X'00000008', X'00000868'.
If the CSD is the only file using those logstreams, CICS disconnects from the log when you end the
CEDA transaction. The next time you run a CEDA transaction, CICS reconnects to the log stream
and the z/OS System Logger allocates and formats a new staging data set.
BACKOUTONLY
CSD recovery is limited to file backout only. If you specify backout for the CSD, CICS uses the
system log to record before images for backout purposes.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
```
**48**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDRLS.......................................................................................................................................................

```
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
CSDRLS={NO|YES}
Valid values are as follows:
NO
The CSD is opened in non-RLS mode, as specified on the CSDLSRNO parameter.
YES
The CSD is opened in RLS mode. This enables you to update the CSD concurrently from several
CICS regions, provided all the regions specify CSDRLS=YES. If a CICS region opens the CSD in RLS
mode, another CICS region cannot open it in non-RLS mode. The first CICS region to open the CSD
in a sysplex with SMSVSAM determines the access mode for all regions.
Your CSD must be defined to support RLS access: the IMBED option must not be specified, and
recovery attributes must be defined in the VSAM catalog. Definitions required for VSAM RLS support
explains the data set characteristics required to support RLS access. If your CSD does not meet these
requirements, it will fail to open.
If you specify both RLS and local shared resource (CSDLSRNO= number ), RLS takes precedence.
If you specify CSDRLS=YES, the CSDRECOV , CSDFRLOG , and CSDJID parameters are ignored. You
must specify the recovery attributes for an RLS-mode CSD in the ICF catalog entry for the CSD.
Note: If you define a recoverable CSD for RLS-mode access, you have to quiesce all RLS activity
against the CSD before you can update the CSD using the CSD update batch utility program
DFHCSDUP. You can use the SET DSNAME QUIESCE command to do this, to ensure that no CEDA,
CEDB, or CEDC transactions can run until you unquiesce the data set on completion of the batch job.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
```
```
Chapter 1. System initialization parameter summary   49
```

```
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CSDSTRNO.................................................................................................................................................

```
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
CSDSTRNO={ 6 |number}
When the number of requests reaches the CSDSTRNO value, CICS automatically queues any additional
requests until one of the active requests terminates.
CICS requires two strings per CSD user, and you can increase the CSDSTRNO value, in multiples of two,
to allow more than one concurrent CEDA user.
See Multiple users of the CSD within a CICS region (non-RLS) before you code this parameter.
This parameter is effective only on a CICS cold or initial start. On a warm or emergency restart, file
resource definitions for the CSD are recovered from the global catalog. However, you can redefine the
number of strings for the CSD dynamically with an EXEC CICS SET FILE command.
6
The default number of concurrent requests for the CSD is 6.
number
This number must be a multiple of 2, in the range 2 through 254.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
**50**   CICS TS for z/OS: System Initialization Parameter Reference


```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
CSD-related system initialization parameters
The CSDACC system initialization parameter
The CSDACC system initialization parameter specifies the type of access to the CSD to be permitted to this
CICS region.
The CSDBKUP system initialization parameter
The CSDBKUP system initialization parameter specifies whether or not the CSD is eligible for the backup-
while-open (BWO) facility.
The CSDBUFND system initialization parameter
The CSDBUFND system initialization parameter specifies the number of buffers to be used for CSD data.
The CSDBUFNI system initialization parameter
The CSDBUFNI system initialization parameter specifies the number of buffers to be used for the CSD
index.
The CSDDISP system initialization parameter
The CSDDISP system initialization parameter specifies the disposition of the data set to be allocated to
the CSD.
The CSDDSN system initialization parameter
The CSDDSN system initialization parameter specifies the 1-44 character JCL data set name (DSNAME) to
be used for the CSD.
The CSDFRLOG system initialization parameter
The CSDFRLOG system initialization parameter specifies a number that corresponds to the journal name
that CICS uses to identify the forward recovery log stream for the CSD.
The CSDINTEG system initialization parameter
The CSDINTEG system initialization parameter specifies the level of read integrity for the CSD if it is
accessed in RLS mode.
The CSDJID system initialization parameter
The CSDJID system initialization parameter specifies the journal identifier of the journal that you want
CICS to use for automatic journaling of file requests against the CSD.
The CSDLSRNO system initialization parameter
The CSDLSRNO system initialization parameter specifies whether the CSD is to be associated with a local
shared resource (LSR) pool.
The CSDRECOV system initialization parameter
The CSDRECOV system initialization parameter specifies whether the CSD is a recoverable file.
The CSDRLS system initialization parameter
The CSDRLS system initialization parameter specifies whether CICS is to access the CSD in RLS mode.
The CSDSTRNO system initialization parameter
The CSDSTRNO system initialization parameter specifies the number of concurrent requests that can be
processed against the CSD.
```
### CWAKEY.....................................................................................................................................................

```
The CWAKEY system initialization parameter specifies the storage key for the common work area (CWA) if
you are operating CICS with storage protection ( STGPROT=YES ).
CWAKEY={USER|CICS}
You specify how much storage you want for the CWA on the WRKAREA parameter. The permitted
values are USER (the default), or CICS:
USER
CICS obtains storage for the CWA in user key. This allows a user program executing in any key to
modify the CWA.
```
```
Chapter 1. System initialization parameter summary   51
```

#### CICS

```
CICS obtains storage for the CWA in CICS key. This means that only programs executing in CICS
key can modify the CWA, and user-key programs have read-only access.
If CICS is running without storage protection, the CWAKEY parameter is ignored, and the CWA is
always allocated from CICS-key storage.
Related concepts
How you can protect CICS storage
Related tasks
Setting up storage protection
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The STGPROT system initialization parameter
The STGPROT system initialization parameter specifies whether you want storage protection to operate in
the CICS region.
```
### DAE.............................................................................................................................................................

```
The DAE system initialization parameter specifies the default DAE action when new system dump table
entries are created.
DAE={NO|YES}
Valid values are as follows:
NO
New system dump table entries are created with DAEOPTION(NODAE). This means that the
system dump is not suppressed by the z/OS Dump Analysis and Elimination (DAE) component.
However, the SUPPRESS and SUPPRESSALL options in the ADYSETxx parmlib member are
controlled by the VRADAE and VRANODAE keys in the SDWA. They might lead to dump
suppression even though NODAE is set here. For information about these options, see z/OS MVS
Diagnosis: Tools and Service Aids.
YES
New system dump table entries are created with DAEOPTION(DAE). This means that the system
dump is eligible for suppression by the z/OS DAE component.
When SET SYSDUMPCODE ADD is specified, if you do not also specify DAEOPTION, NODAE is used by
default, regardless of the setting of the DAE system initialization parameter.
For more information about the DAEOPTION option, see SET SYSDUMPCODE.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Using dumps in problem determination
Detecting and avoiding duplicate system dumps
```
**52**   CICS TS for z/OS: System Initialization Parameter Reference


### DATFORM...................................................................................................................................................

```
The DATFORM system initialization parameter specifies the external date display standard that you want
to use for CICS date displays.
DATFORM={MMDDYY|DDMMYY|YYMMDD}
An appropriate indicator setting is made in the CSA. It is examined by CICS supplied system service
programs that display a Gregorian date. CICS maintains the date in the form 0CYYDDD in the CSA
(where C=0 for years 19xx, 1 for years 20xx, and so on; YY=year of century; and DDD=day of year),
and converts it to the standard you specify for display.
The DATFORM option selects the order in which the date is to be displayed. It does not select the
format of the year. Both YY and YYYY formats are displayed.
MMDDYY
The date is in the form of month-day-year, MMDDYY and MMDDYYYY.
DDMMYY
The date is in the form of day-month-year, DDMMYY and DDMMYYYY.
YYMMDD
The date is in the form of year-month-day, YYMMDD and YYYYMMDD.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## DB2CONN...................................................................................................................................................

```
The DB2CONN system initialization parameter specifies whether you want CICS to start the Db2
connection automatically during initialization.
DB2CONN={NO|YES}
Valid values are as follows:
NO
Do not automatically invoke DFHD2CM0, the CICS Db2 attach program, during initialization.
YES
Invoke the CICS Db2 attach program, DFHD2CM0, automatically during CICS initialization. The
other information CICS needs for starting the attachment is taken from CICS Db2 connection
resource definitions installed from the CSD.
Recommendation: Specifying DB2CONN=YES is the recommended alternative to specifying the CICS
Db2 attach programs in the CICS post-initialization program list table (PLT).
Related tasks
Defining the CICS Db2 connection
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Overview of the CICS Db2 interface
Administering the CICS Db2 interface
Accounting and monitoring in a CICS Db2 environment
Troubleshooting Db2
```
```
Chapter 1. System initialization parameter summary   53
```

## DBCTLCON.................................................................................................................................................

```
The DBCTLCON system initialization parameter specifies whether you want CICS to start the DBCTL
connection automatically during initialization.
DBCTLCON={NO|YES}
Valid values are as follows:
NO
Do not automatically invoke DFHDBCON, the CICS DBCTL attach program, during initialization.
YES
Invoke the CICS DBCTL attach program, DFHDBCON, automatically during CICS initialization. The
other information CICS needs for starting the attachment, such as the DRA startup table suffix or
the DBCTL subsystem name, is taken from an INITPARM system initialization parameter.
Specifying DBCTLCON=YES means you don't need to define the DBCTL attach program in the CICS
post-initialization program list table (PLT).
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Overview of Database Control (DBCTL)
Installing DBCTL, and defining CICS and IMS system resources
Operations with DBCTL
Monitoring IMS
Troubleshooting DBCTL
```
## DEBUGTOOL...............................................................................................................................................

```
The DEBUGTOOL system initialization parameter specifies whether you want to use debugging profiles to
select the programs that will run under the control of a debugging tool.
DEBUGTOOL={NO|YES}
The following debugging tools use debugging profiles:
```
- Debug Tool, for compiled language application programs (programs written in COBOL, PL/I, C, C++
    and Assembler)
- Remote debugging tools (for compiled language application programs and Java™ programs)
Other debugging mechanisms, such as the CICS Execution Diagnostic Facility (CEDF) do not use
debugging profiles.
**NO**
    Specifies that you do not want to use CICS debugging profiles to select the programs that will run
    under the control of a debugger tool.
**YES**
    Specifies that you want to use CICS debugging profiles to select the programs that will run under
    the control of a debugging tool.
For more information, see Debugging profiles.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the

**54**   CICS TS for z/OS: System Initialization Parameter Reference


```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
CEDF, CEDG, CEDX, and CEDY - CICS execution diagnostic facility transactions
```
## DFLTUSER...................................................................................................................................................

```
The DFLTUSER system initialization parameter specifies the RACF user ID of the default user; that is, the
user whose security attributes are used to protect CICS resources in the absence of other, more specific,
user identification.
DFLTUSER={CICSUSER|userid}
For example, except in the case of terminals defined with preset security, the security attributes of the
default user are assigned to terminal users who do not sign on.
The specified user ID must be defined to RACF if you are using external security (that is, you have
specified the system initialization parameter SEC=YES ).
The specified user ID is signed on during CICS initialization. If it cannot be signed on, CICS fails to
initialize.
Restriction: You can specify the DFLTUSER parameter in the SIT, PARM, or SYSIN only.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
CICS system resource security
Defining the default CICS user ID to RACF
CICS initialization failures related to security
```
## DIP..............................................................................................................................................................

```
The DIP system initialization parameter specifies whether the batch data interchange program, DFHDIP,
is to be included. This program supports the batch controller functions of the IBM 3790 Communication
System and the IBM 3770 Data Communication System. Support is provided for the transmit, print,
message, user, and dump data sets of the 3790 system.
The data interchange program is designed as a function manager for Systems Network Architecture (SNA)
devices. It is invoked via DFHEDI for command-level requests, or internally by the basic mapping support
(BMS) routines using the DFHDI macro. For details about the batch data interchange program DFHDIP,
see Component reference: Data interchange program.
DIP={NO|YES}
For the effect of this parameter, see Defining CICS resource table and module keywords.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
```
```
Chapter 1. System initialization parameter summary   55
```

```
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## DISMACP....................................................................................................................................................

```
The DISMACP system initialization parameter specifies whether CICS is to disable any transaction that
terminates abnormally with an ASRD or ASRE abend.
DISMACP={YES|NO}
DISMACP=YES has no effect if the ASRD or ASRE abend is handled by an active abend exit. An abend
might be caused by a user program invoking a CICS macro, or referencing the common service area
(CSA), or the task control area (TCA).
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
ASRD
ASRE
Related information
Dealing with transaction abend codes
Transaction abend codes: AEYD, AICA, ASRA, ASRB, and ASRD
```
## DOCCODEPAGE..........................................................................................................................................

```
The DOCCODEPAGE system initialization parameter specifies the default host code page to be used by the
document domain.
DOCCODEPAGE={ 037 |codepage}
The codepage is a field of up to 8 characters. If codepage value is not specified, the default
doccodepage is set to 037.
The standard CICS form of a host code page name consists of the code page number (or more
generally CCSID) written using 3 to 5 decimal digits as necessary then padded with trailing spaces to
8 characters. For code page 37, which is fewer than 3 digits, the standard form is 037. CICS accepts
any decimal number of up to 8 digits (padded with trailing spaces) in the range 1 to 65535 as a code
page name, even if it is not in the standard form.
The DOCCODEPAGE parameter must specify an EBCDIC-based code page if any symbol processing is
required, as the delimiters used for symbol and symbol list processing are assumed to be in EBCDIC.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## DSALIM.......................................................................................................................................................

```
The DSALIM system initialization parameter specifies the upper limit of the total amount of storage within
which CICS can allocate the individual dynamic storage areas (DSAs) that reside in 24-bit storage.
To control the equivalent limit for extended dynamic storage areas, see EDSALIM system initialization
parameter.
DSALIM={5M| number }
Valid values are as follows:
```
**56**   CICS TS for z/OS: System Initialization Parameter Reference


#### 5M

```
The default DSALIM value is 5 MB.
number
A value in the range 2 MB to 16 MB, in multiples of 256 KB. If the size specified is not a multiple
of 256 KB, CICS rounds the value up to the next multiple. You can specify number as a number of
bytes, a whole number of kilobytes, or a whole number of megabytes. Use the letter M to indicate
that the value represents a whole number of megabytes (for example, 4 M). Use the letter K to
indicate that the value represents a whole number of kilobytes (for example, 4096 K), in which
case the number is rounded up to the number of megabytes. If transaction isolation is active, the
extent size for the user DSA is 1 MB and each user DSA extent must be aligned on a megabyte
boundary. Otherwise, the allocation is in 256 KB extents for all the 24-bit DSAs.
From the storage that you specify by using DSALIM , CICS allocates the dynamic storage areas that reside
in 24-bit storage (see CICS dynamic storage areas (DSAs)).
If your installation is constrained for 24-bit storage, set a value for the DSALIM parameter equivalent to
the sum of the 24-bit DSAs. If you have sufficient virtual storage to allow a greater value for DSALIM , see
Estimating, checking, and setting DSALIM for considerations. The maximum value that you can specify for
DSALIM is limited by the following factors:
```
- The configuration of your MVS storage, which governs how much private storage remains below the line.
- The size that you specified for the CICS region on the z/OS **REGION** parameter in the CICS job or
    procedure. The **DSALIM** value must be smaller than the REGION size specified for the CICS job, or
    smaller than the limit specified in the IEFUSI exit.
- The amount of MVS storage, outside the DSAs, that you require to satisfy z/OS GETMAIN requests for
    24-bit storage.
If you change the **DSALIM** value while CICS is running, the change is cataloged in the local catalog. If
**DSALIM** is specified in the system initialization table, the cataloged value that is specified by the change
overrides the value of the **DSALIM** system initialization parameter on an initial, cold, or warm start. The
cataloged value is not used if you specify **DSALIM** as a system initialization parameter override (for
example, in SYSIN), or if you reinitialize the CICS catalog data sets.

## DSHIPIDL...................................................................................................................................................

```
The DSHIPIDL system initialization parameter specifies the minimum time, in hours, minutes, and
seconds, that an inactive shipped terminal definition must remain installed in this region. When the
timeout delete mechanism is invoked, only those shipped definitions that have been inactive for longer
than the specified time are deleted. You can use this parameter in a transaction routing environment, on
the application-owning and intermediate regions, to prevent terminal definitions having to be reshipped
because they have been deleted prematurely.
In a transaction routing environment, redundant shipped terminal definitions should not be permitted to
persist for performance and security considerations. The CRMF transaction periodically scans the shipped
terminal definitions in the AOR and flags redundant shipped terminal definitions. The system initialization
parameters DSHIPINT and DSHIPIDL control the amount of time for which a redundant shipped terminal
definition is allowed to survive and the frequency at which shipped terminal definitions are tested for
redundancy. For additional details, see Controlling the deletion of shipped terminal definitions (DSHIPINT
and DSHIPIDL).
DSHIPIDL={020000|hhmmss}
The default minimum idle time is 2 hours.
hhmmss
A 1- to 6-digit number in the range 0-995959. Numbers that have fewer than six digits are padded
with leading zeros.
Related reference
“System initialization parameter summary” on page 1
```
```
Chapter 1. System initialization parameter summary   57
```

```
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The DSHIPINT system initialization parameter
The DSHIPINT system initialization parameter specifies the interval between invocations of the timeout
delete mechanism. The timeout delete mechanism removes any shipped terminal definitions that have
not been used for longer than the time specified by the DSHIPIDL system initialization parameter.
```
## DSHIPINT...................................................................................................................................................

```
The DSHIPINT system initialization parameter specifies the interval between invocations of the timeout
delete mechanism. The timeout delete mechanism removes any shipped terminal definitions that have
not been used for longer than the time specified by the DSHIPIDL system initialization parameter.
In a transaction routing environment, redundant shipped terminal definitions should not be permitted to
persist for performance and security considerations. The CRMF transaction periodically scans the shipped
terminal definitions in the AOR and flags redundant shipped terminal definitions. The system initialization
parameters DSHIPINT and DSHIPIDL control the amount of time for which a redundant shipped terminal
definition is allowed to survive and the frequency at which shipped terminal definitions are tested for
redundancy. For additional details, see Controlling the deletion of shipped terminal definitions (DSHIPINT
and DSHIPIDL).
DSHIPINT={120000|0|hhmmss}
You can use this parameter in a transaction routing environment, on the application-owning and
intermediate regions, to control:
```
- How often the timeout delete mechanism is invoked
- The approximate time of day at which a mass delete operation is to take place, relative to CICS
    startup
    **Note:** For more flexible control over when mass delete operations take place, you can use a **CEMT**
    **SET DELETSHIPPED** or **EXEC CICS SET DELETSHIPPED** command to reset the interval. (The
    revised interval starts _from the time the command is issued_ , **not** from the time the remote delete
    mechanism was last invoked, nor from CICS startup.)
**0**
    The timeout delete mechanism is not invoked. You might set this value in a terminal-owning
    region, or if you are not using shipped definitions.
**hhmmss**
    A 1- to 6-digit number in the range 1-995959. Numbers that have fewer than six digits are padded
    with leading zeros.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The DSHIPIDL system initialization parameter
The **DSHIPIDL** system initialization parameter specifies the minimum time, in hours, minutes, and
seconds, that an inactive shipped terminal definition must remain installed in this region. When the
timeout delete mechanism is invoked, only those shipped definitions that have been inactive for longer
than the specified time are deleted. You can use this parameter in a transaction routing environment, on
the application-owning and intermediate regions, to prevent terminal definitions having to be reshipped
because they have been deleted prematurely.

**58**   CICS TS for z/OS: System Initialization Parameter Reference


## DSRTPGM...................................................................................................................................................

```
The DSRTPGM system initialization parameter specifies the name of a distributed routing program. The
distributed routing program must be specified in the DSRTPGM parameter for all routing and potential
target regions.
DSRTPGM={NONE|DFHDSRP| program-name |EYU9XLOP}
Valid values are as follows:
DFHDSRP
The CICS sample distributed routing program.
EYU9XLOP
The CICSPlex SM routing program.
NONE
No routing program is invoked.
program-name
The name of a user-written program.
Note: See also the DTRPGM parameter, which is used to name the dynamic routing program.
```
```
What transactions are eligible for dynamic routing
The distributed routing program can dynamically route the following:
```
- Eligible CICS business transaction services (BTS) processes and activities
    For information about which BTS processes and activities are eligible for dynamic routing, see
    Administering BTS.
- Eligible non-terminal-related **EXEC CICS START** requests
    For information about which non-terminal-related START requests are eligible for dynamic routing, see
    Routing transactions invoked by START commands.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

## DTRPGM.....................................................................................................................................................

```
The DTRPGM system initialization parameter specifies the name of a dynamic routing program.
The program can dynamically route transactions initiated from user terminals, transactions initiated
by eligible terminal-related EXEC CICS START commands, and eligible program-link requests. For
information about which transactions started by EXEC CICS START commands, and which program-link
requests, are eligible for dynamic routing, see Introduction to CICS dynamic routing.
DTRPGM={DFHDYP|EYU9XLOP|NONE| program-name }
Valid values are as follows:
DFHDYP
The CICS-supplied routing program. This program is the default.
EYU9XLOP
The CICSPlex SM routing program.
NONE
No routing program is invoked.
program-name
The name of a user-written program.
```
```
Chapter 1. System initialization parameter summary   59
```

```
See also the DSRTPGM parameter, which is used to name the distributed routing program.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## DTRTRAN....................................................................................................................................................

```
The DTRTRAN system initialization parameter specifies the name of the transaction definition that you
want CICS to use for dynamic transaction routing.
DTRTRAN={CRTX| name |NO}
This is intended primarily for use in a CICS terminal-owning region, although you can also use it in an
application-owning region when you want to daisy-chain transaction routing requests. In a dynamic
transaction routing environment, the transaction defined for DTRTRAN must be installed in the CICS
terminal-owning regions if you want to eliminate the need for resource definitions for individual
transactions.
Note: DTRTRAN does not apply to non-terminal EXEC CICS START requests where the distributed
routing program is invoked.
The transaction name is stored in the catalog for recovery during CICS restarts.
CRTX
This is the default dynamic transaction definition. It is the name of the CICS-supplied sample
transaction resource definition provided in the CSD group DFHISC.
name
The name of your own dynamic transaction resource definition that you want CICS to use for
dynamic transaction routing.
NO
The dynamic transaction routing program is not invoked when a transaction definition cannot be
found.
For information about the CICS-supplied sample transaction resource definition, CRTX, and about
defining your own dynamic transaction routing definition, see Dynamic transaction routing.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## DUMP..........................................................................................................................................................

```
The DUMP system initialization parameter specifies whether the CICS dump domain is to take SDUMPs.
DUMP={YES|NO|TABLEONLY} (active and alternate)
Valid values are as follows:
YES
SDUMPs are produced, unless suppressed by the options specified in the CICS system dump table
or by the z/OS system defaults.
NO
SDUMPs are suppressed.
Note: This does not prevent the CICS kernel from taking SDUMPs.
```
**60**   CICS TS for z/OS: System Initialization Parameter Reference


#### TABLEONLY

```
SDUMPs are suppressed except those which have an explicit entry in the dump table with options
that allow a dump to be taken. This allows for targeted capturing of dumps for a specific error
situation. Any dump table entries added implicitly by CICS will not result in a dump being taken.
For information about the SDUMP macro and the associated dump data sets, see z/OS MVS Diagnosis:
Tools and Service Aids.
Related tasks
Defining system dump data sets
Taking CICS system dumps
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Using dumps in problem determination
```
## DUMPDS.....................................................................................................................................................

```
Transaction dumps go to a pair of CICS BSAM data sets, with DD names DFHDMPA and DFHDMPB. The
DUMPDS system initialization parameter specifies the transaction dump data set that is to be opened
during CICS initialization. A transaction dump data set must be OPEN if it is to be written to.
DUMPDS={AUTO|A|B}
Valid values are as follows:
AUTO
For all emergency or warm starts, CICS opens the transaction dump data set that was not in use
when the previous CICS run terminated. This information is obtained from the CICS local catalog.
If you specify AUTO, or let it default, code DD statements for both of the transaction dump data
sets, DFHDMPA and DFHDMPB, in your CICS startup job stream.
A
CICS opens transaction dump data set DFHDMPA.
B
CICS opens transaction dump data set DFHDMPB.
Tip: You can use the CEMT SET DUMPDS transaction or an EXEC CICS SET DUMPDS command to switch
the transaction dump data sets when CICS is running.
Related concepts
Where dumps are written
Related tasks
Defining transaction dump data sets
Printing the transaction dump data sets
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The DUMPSW system initialization parameter
```
```
Chapter 1. System initialization parameter summary   61
```

```
Transaction dumps go to a pair of CICS BSAM data sets, with DD names DFHDMPA and DFHDMPB. The
DUMPSW system initialization parameter specifies whether you want CICS to switch automatically to the
next transaction dump data set when the first is full.
```
## DUMPSW....................................................................................................................................................

```
Transaction dumps go to a pair of CICS BSAM data sets, with DD names DFHDMPA and DFHDMPB. The
DUMPSW system initialization parameter specifies whether you want CICS to switch automatically to the
next transaction dump data set when the first is full.
DUMPSW={NO|NEXT|ALL}
Valid values are as follows:
NO
Disables the CICS autoswitch facility. If the transaction dump data set opened during initialization
becomes full, CICS issues a console message to notify the operator. If you want to switch to
the alternate data set, you must do so manually using the CEMT or EXEC CICS SET DUMPDS
SWITCH command.
NEXT
Enables the autoswitch facility to switch to the next data set at end of file of the data set opened
during initialization. Coding NEXT permits one switch only. If you want to switch to the alternate
data set again, you must do so manually using CEMT or EXEC CICS SET DUMPDS SWITCH
command. If you specify NEXT, code DD statements for both of the transaction dump data sets,
DFHDMPA and DFHDMPB, in your CICS startup job stream.
ALL
Enables the autoswitch facility to switch to the inactive data set at every end of file. Specifying ALL
enables continuous switching between the two dump data sets, DFHDMPA and DFHDMPB, and
whenever a data set is full, it is closed and the other data set is opened.
Related concepts
Where dumps are written
Related tasks
Defining transaction dump data sets
Printing the transaction dump data sets
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The DUMPDS system initialization parameter
Transaction dumps go to a pair of CICS BSAM data sets, with DD names DFHDMPA and DFHDMPB. The
DUMPDS system initialization parameter specifies the transaction dump data set that is to be opened
during CICS initialization. A transaction dump data set must be OPEN if it is to be written to.
```
## DURETRY....................................................................................................................................................

```
The DURETRY system initialization parameter specifies, in seconds, the total time that CICS is to continue
trying to obtain a system dump using the SDUMP macro.
DURETRY={ 30 |number-of-seconds|0}
DURETRY allows you to control whether, and for how long, CICS is to reissue the SDUMP macro if
another address space in the same MVS system is already taking an SDUMP when CICS issues an
SDUMP request.
In the event of an SDUMP failure, CICS responds, depending on the reason for the failure, as follows:
```
**62**   CICS TS for z/OS: System Initialization Parameter Reference


- If MVS is already taking an SDUMP for another address space, and the DURETRY parameter is
    nonzero, CICS issues an MVS STIMERM macro to wait for five seconds, before retrying the SDUMP.
    CICS issues a message to say that it is waiting for five seconds before retrying the SDUMP. After five
    seconds CICS issues another message to say that it is retrying the SDUMP request.
- If the SDUMP fails for any other reason, such as no SYS1.DUMP data sets being available, or I/O
    errors preventing completion of the dump, CICS issues a message to inform you that the SDUMP has
    failed, and to give the reason why.
**30**
    30 seconds allows CICS to retry up to 6 times (once every 5 seconds), if the cause of failure is that
    another region is taking an SDUMP.
**number-of-seconds**
    Code the total number of seconds (up to 32767) during which you want CICS to continue retrying
    the SDUMP macro if the reason for failure is that another region is taking an SDUMP. CICS retries
    the SDUMP, once every five seconds, until successful or until retries have been made over a period
    equal to or greater than the DURETRY value.
**0**
    Code a zero value if you do not want CICS to retry the SDUMP macro.
**Related reference**
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a **PARM** parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.

## ECDSASZE..................................................................................................................................................

```
The ECDSASZE system initialization parameter specifies the size of the ECDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
ECDSASZE={0K|number}
Valid values are as follows:
0 (zero)
The size of the ECDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the ECDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 1073741824 bytes in multiples of 1048576
bytes (1 MB).. If the value you specify is not a multiple of 1 MB, CICS rounds up the value to the
next multiple.
You can specify number as a number of bytes, a whole number of kilobytes, or a whole number of
megabytes. Use the letter M to indicate that the value represents a whole number of megabytes
(for example, 4 M). Use the letter K to indicate that the value represents a whole number of
kilobytes (for example, 4096 K), in which case the number is rounded up to the number of
megabytes.
Restriction: You can specify the ECDSASZE parameter in PARM, SYSIN, or CONSOLE only.
Related concepts
CICS dynamic storage areas (DSAs)
```
```
Chapter 1. System initialization parameter summary   63
```

```
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
```
## EDSALIM....................................................................................................................................................

```
The EDSALIM system initialization parameter specifies the upper limit of the total amount of storage
within which CICS can allocate the individual extended dynamic storage areas (E xx DSAs) that reside in
31-bit (above-the-line) storage; that is, above 16 MB but below 2 GB.
To control the equivalent limit for dynamic storage areas, use the DSALIM system initialization parameter.
EDSALIM={800M| number}
800M
The default EDSALIM value is 800 MB.
number
A value in the range 64 MB (the minimum required to start a CICS region) through 2047 MB, in
multiples of 1 MB. If the size specified is not a multiple of 1 MB, CICS rounds the value up to
the next multiple. You can specify number as a number of bytes, a whole number of kilobytes,
or a whole number of megabytes. Use the letter M to indicate that the value represents a whole
number of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a
whole number of kilobytes (for example, 4096 K), in which case the number is rounded up to the
number of megabytes. The extent size for the extended DSAs is 1 MB.
From the storage that you specify by using EDSALIM , CICS allocates the extended dynamic storage areas
that reside in 31-bit (above-the-line) storage. For information, see CICS dynamic storage areas (DSAs).
Set the value for the EDSALIM parameter as large as you can after consideration of other areas, especially
z/OS storage. For considerations, see Estimating, checking, and setting EDSALIM. The maximum value
that you can specify for EDSALIM is limited by the following factors:
```
- The size that you specified for the CICS region on the z/OS **REGION** parameter in the CICS job or
    procedure. The **EDSALIM** value must be smaller than the REGION size specified for the CICS job, or
    smaller than the limit specified in the IEFUSI exit.
- The amount of z/OS storage, outside the extended DSAs, that you require to satisfy z/OS **GETMAIN**
    requests for 31-bit (above-the-line) storage.
If you change the limit for extended DSAs while CICS is running, the change is cataloged in the local
catalog. If **EDSALIM** is specified in the system initialization table, the cataloged value that is specified by
the change overrides the value of the **EDSALIM** system initialization parameter on an initial, cold, or warm
start. The cataloged value is not used if you specify **EDSALIM** as a system initialization parameter override
(for example, in SYSIN), or if you reinitialize the CICS catalog data sets.

## EODI...........................................................................................................................................................

```
The EODI system initialization parameter specifies the end-of-data indicator for input from sequential
devices.
Sequential terminals provide simulation of actual terminals, and can be used before the actual terminals
become available. Sequential terminals can also be used during the testing of new applications. When
defining sequential devices, you can use a pair of input and output sequential data sets to simulate a
terminal to CICS. Each statement in the input file must end with a character representing X'E0'. The
standard EBCDIC symbol for this end-of-data hexadecimal value is a backslash (\) character, and this
is the character defined to CICS in the pregenerated system. You can redefine this for your installation
on the EODI system initialization parameter. For details and examples, see Defining sequential (BSAM)
devices.
```
**64**   CICS TS for z/OS: System Initialization Parameter Reference


```
EODI={E0|xx}
The characters "xx" represent two hexadecimal digits in the range 01 through FF. The default value is
X'E0', which represents the standard EBCDIC backslash symbol (\).
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Using sequential terminal support
Terminal control table (TCT)
```
## EPCDSASZE................................................................................................................................................

```
The EPCDSASZE parameter specifies the size of the EPCDSA dynamic storage area. Message
DFHSM0136I at initialization shows the value that is set.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
EPCDSASZE={ 0 | number }
Valid values are as follows:
0 (zero)
The size of the EPCDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the EPCDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 1073741824 bytes in multiples of 1048576
bytes (1 MB). If the value you specify is not a multiple of 1 MB, CICS rounds up the value to
the next multiple.You can specify number as a number of bytes, a whole number of kilobytes,
or a whole number of megabytes. Use the letter M to indicate that the value represents a whole
number of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a
whole number of kilobytes (for example, 4096 K), in which case the number is rounded up to the
number of megabytes.
Restriction: You can specify the EPCDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## EPUDSASZE................................................................................................................................................

```
The EPUDSASZE parameter specifies the size of the EPUDSA dynamic storage area. Message
DFHSM0136I at initialization shows the value that is set.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
EPUDSASZE={ 0 | number }
Valid values are as follows:
0 (zero)
The size of the EPUDSA dynamic storage area size can change dynamically. Zero is the default.
```
```
Chapter 1. System initialization parameter summary   65
```

```
number
A non-zero value specifies that the size of the EPUDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 1073741824 bytes in multiples of 1048576
bytes (1 MB). If the value you specify is not a multiple of 1 MB, CICS rounds up the value to
the next multiple.You can specify number as a number of bytes, a whole number of kilobytes,
or a whole number of megabytes. Use the letter M to indicate that the value represents a whole
number of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a
whole number of kilobytes (for example, 4096 K), in which case the number is rounded up to the
number of megabytes.
Restriction: You can specify the EPUDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## ERDSASZE..................................................................................................................................................

```
The ERDSASZE system initialization parameter specifies the size of the ERDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
ERDSASZE={0K|number}
Valid values are as follows:The default size is 0 indicating that the DSA size can change dynamically. A
non-zero value indicates that the DSA size is fixed.
0 (zero)
The size of the ERDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the ERDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 1073741824 bytes in multiples of 1048576
bytes (1 MB). If the value you specify is not a multiple of 1 MB, CICS rounds up the value to
the next multiple.You can specify number as a number of bytes, a whole number of kilobytes,
or a whole number of megabytes. Use the letter M to indicate that the value represents a whole
number of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a
whole number of kilobytes (for example, 4096 K), in which case the number is rounded up to the
number of megabytes.
Restriction: You can specify the ERDSAZSE parameter in PARM, SYSIN, or CONSOLE only.
```
## ESDSASZE..................................................................................................................................................

```
The ESDSASZE system initialization parameter specifies the size of the ESDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
ESDSASZE={0K|number}
Valid values are as follows:The default size is 0 indicating that the DSA size can change dynamically. A
non-zero value indicates that the DSA size is fixed.
0 (zero)
The size of the ESDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the ESDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 1073741824 bytes in multiples of 1048576
```
**66**   CICS TS for z/OS: System Initialization Parameter Reference


```
bytes (1 MB). If the value you specify is not a multiple of 1 MB, CICS rounds up the value to
the next multiple.You can specify number as a number of bytes, a whole number of kilobytes,
or a whole number of megabytes. Use the letter M to indicate that the value represents a whole
number of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a
whole number of kilobytes (for example, 4096 K), in which case the number is rounded up to the
number of megabytes.
Restriction: You can specify the ESDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## ESMEXITS...................................................................................................................................................

```
The ESMEXITS system initialization parameter specifies whether installation data is to be passed through
the RACROUTE interface to the external security manager (ESM) for use in exits written for the ESM.
ESMEXITS={NOINSTLN|INSTLN}
Valid values are as follows:
NOINSTLN
The INSTLN parameter is not used in RACROUTE macros.
INSTLN
CICS-related and installation-supplied data is passed to the ESM using the INSTLN parameter of
the RACROUTE macro. For programming information, including the format of the data passed, see
Invoking an external security manager. This data is intended for use in exits written for the ESM.
Restriction: You can specify the ESMEXITS parameter in the SIT only.
```
## EUDSASZE..................................................................................................................................................

```
The EUDSASZE system initialization parameter specifies the size of the EUDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 31-bit
storage (above the line) is specified by the EDSALIM system initialization parameter system initialization
parameter. You must allow at least 1 MB for each DSA in 31-bit storage for which you have not set a size.
See DSALIM system initialization parameter.
EUDSASZE={0K|number}
The default size is 0 indicating that the DSA size can change dynamically. A non-zero value indicates
that the DSA size is fixed.
number
Specify number as an amount of storage in the range 0 to 1073741824 bytes in multiples of
1048576 bytes (1MB). If the size specified is not a multiple of 1MB, CICS rounds the value up to
the next multiple.
You can specify number in bytes (for example, 4194304), or as a whole number of kilobytes (for
example, 4096K), or a whole number of megabytes (for example, 4M).
Restriction: You can specify the EUDSAZSE parameter in PARM, SYSIN, or CONSOLE only.
```
## FCT.............................................................................................................................................................

```
The file control table (FCT) describes to CICS the Basic Direct Access Method (BDAM) user files that are
processed by file management. The FCT system initialization parameter specifies the suffix of the file
control table to be used.
FCT={NO|xx|YES}
This parameter is effective only on a CICS cold or initial start. CICS does not load an FCT on a warm or
emergency restart, and all file resource definitions are recovered from the global catalog.
```
```
Chapter 1. System initialization parameter summary   67
```

```
You use the DFHFCT macros to specify file characteristics, and some of the characteristics of BDAM
data sets referenced by the files. For information about coding the macros for this table, see File
control table (FCT).
You can use a mixture of macro definitions and RDO definitions for files in your CICS region. However,
your FCT should contain definitions for only BDAM files to be loaded on a CICS cold start. Other
types of files are loaded from their file definitions in RDO groups specified in the GRPLIST system
initialization parameter. Any definitions in the FCT other than for BDAM files are ignored.
```
## FCQRONLY..................................................................................................................................................

```
The FCQRONLY system initialization parameter specifies whether you want CICS to force all file control
requests to run under the CICS QR TCB. This parameter applies to file control requests that access VSAM
RLS files and local VSAM LSR files.
FCQRONLY={YES|NO}
Valid values are as follows:
NO
File Control requests are treated as threadsafe and are run on an open TCB to avoid unnecessary
TCB switching. For CONCURRENCY(REQUIRED) programs the request runs on an open TCB. For
CONCURRENCY(THREADSAFE) programs the request runs on whatever TCB is being used at the
time of the request.
YES
File control requests are treated as non-threadsafe. CICS forces all file control requests to run
under the CICS QR TCB. With all file requests on the QR TCB, CICS can minimize the amount of
locking required at the expense of additional TCB switches if requests are run on open TCBs. YES
is the default.
For a program defined as CONCURRENCY(REQUIRED), if the file control request is run under the
CICS QR TCB, CICS switches back to the open TCB before handing control back to the application
program.
For file-owning regions (FORs), choose an appropriate setting for FCQRONLY :
```
- For FORs where the connections to that region are primarily MRO or ISC connections, these
    requests run on the QR TCB, and CICS runs the mirror program primarily on the QR TCB. Specify
    **FCQRONLY=YES** so that all file control requests are processed on the QR TCB. This setting improves
    performance by avoiding locking, which is unnecessary when all file control requests run on the
    same TCB.
- For FORs where the connections to that region are primarily IPIC connections, these requests run
    on open TCBs, and CICS runs the mirror program on an L8 open TCB whenever possible. Specify
    **FCQRONLY=NO** so that file control requests do not switch to the QR TCB to be processed. This
    setting improves performance by multi-threading file control requests.

## FEPI............................................................................................................................................................

```
The Front End Programming Interface (FEPI) is an integral part of CICS. You can use FEPI to write CICS
applications that simulate terminals to access other CICS or IMS programs. The FEPI system initialization
parameter specifies whether or not you want to use the Front End Programming Interface feature.
FEPI={NO|YES}
Valid values are as follows:
NO
FEPI support is not required. You should specify NO on this parameter (or allow it to default) if you
do not have the feature installed, or if you do not require FEPI support.
YES
You require FEPI support, and CICS is to start the CSZI transaction.
For information about what is required to run FEPI, see FEPI analysis and planning.
```
**68**   CICS TS for z/OS: System Initialization Parameter Reference


## FLDSEP.......................................................................................................................................................

```
The FLDSEP system initialization parameter specifies one through four field-separator characters, each of
which indicates end of field in the terminal input data.
FLDSEP={' '|'xxxx' }
The default is four blanks. The field separator allows you to use transaction identifications of less
than four characters followed by one of the separator characters. When less than four characters are
coded, the parameter is padded with blanks, so that the blank is then a field separator. None of the
specified field separator characters should be part of a transaction identification; in particular, the use
of alphabetic characters as field separators is not recommended.
The character specified in the FLDSEP parameter must not be the same as any character specified
in the FLDSTRT parameter. This means that it is invalid to allow both parameters to take the default
value. Restrictions
If you specify FLDSEP in the SIT, the characters must be enclosed in single quotation marks.
If you specify FLDSEP as a PARM, SYSIN, or CONSOLE parameter, do not enclose the characters in
quotation marks, and the characters you choose must not include an embedded blank, or any of these
characters:
```
```
( ) ' = ,
```
## FLDSTRT.....................................................................................................................................................

```
The FLDSTRT system initialization parameter specifies a single character to be the field-name-start
character for free-form input for built-in functions.
FLDSTRT={' '|'x'}
The default is a blank. The character specified should not be part of a transaction identification; in
particular, the use of alphabetic characters is not recommended.
The character specified in the FLDSTRT parameter must not be the same as any character specified in
the FLDSEP parameter. This means that it is invalid to allow both parameters to take the default value.
Restrictions
If you specify FLDSTRT in the SIT, the parameter must be enclosed in single quotation marks.
If you specify FLDSTRT as a PARM, SYSIN, or CONSOLE parameter, do not enclose the character in
quotation marks, and the character you choose must not be a blank or any of the following characters:
```
```
( ) ' = ,
```
## FORCEQR....................................................................................................................................................

```
The FORCEQR system initialization parameter specifies whether you want CICS to force all CICS API user
application programs that are specified as threadsafe to run under the CICS QR TCB, as if they were
specified as quasi-reentrant programs.
FORCEQR={NO|YES}
This parameter applies to all application programs that are restricted to the current CICS
programming interfaces (that is, programs that specify API(CICSAPI)), and does not apply to any
of the following programs:
```
- Java programs that are run in a JVM
- C/C++ programs using XPLINK
- OPENAPI programs
- Programs defined with CONCURRENCY(REQUIRED)
None of these programs can run on the QR TCB.

```
Chapter 1. System initialization parameter summary   69
```

#### NO

```
CICS honors the CONCURRENCY(THREADSAFE) attribute on program resource definitions, and
allows user application programs to run on an open TCB to avoid unnecessary TCB switching.
YES
CICS forces all CICSAPI user application programs specified with the
CONCURRENCY(THREADSAFE) attribute to run under the CICS QR TCB, as if they were specified
as CONCURRENCY(QUASIRENT) programs
FORCEQR=YES allows you, in a test environment, to run incompletely tested threadsafe application
programs that have proved to be non-threadsafe.
The FORCEQR parameter applies to all programs defined as threadsafe that are not invoked as task-
related user exits, global user exits, or user-replaceable modules.
```
## FSSTAFF.....................................................................................................................................................

```
The FSSTAFF system initialization parameter prevents transactions initiated by function-shipped EXEC
CICS START requests being started against incorrect terminals.
FSSTAFF={YES|NO}
Specify this parameter in an application-owning region (AOR). You might need to code the function-
shipped START affinity (FSSTAFF) parameter in an AOR if all of the following are true:
```
1. The AOR is connected to two or more terminal-owning regions (TORs) that use the same, or a
    similar, set of terminal identifiers.
2. One or more of the TORs issues **EXEC CICS START** requests for transactions in the AOR.
3. The START requests are associated with terminals.
4. You are using shippable terminals, rather than statically defining remote terminals in the AOR.
Consider the following scenario:
Terminal-owning region TOR1 issues an **EXEC CICS START** request for transaction TRAR, which
is owned by region AOR1. It is to be run against terminal T001. Meanwhile, terminal T001 on
region TOR2 has been transaction routing to AOR1; a definition of T001 has been shipped to AOR1
from TOR2. When the START request arrives at AOR1, it is shipped to TOR2, rather than TOR1, for
transaction routing from terminal T001.
To prevent this situation, code YES on the FSSTAFF parameter in the AOR.
**YES**
When a START request is received from a terminal-owning region, and a shipped definition for the
terminal named on the request is already installed in the AOR, the request is always shipped back
to a TOR, for routing, _across the link it was received on_ , irrespective of the TOR referenced in the
remote terminal definition.
If the TOR to which the START request is returned is **not** the one referenced in the installed
remote terminal definition, a definition of the terminal is shipped to the AOR, and the autoinstall
user program is called. Your autoinstall user program can then allocate an _alias_ termid in the AOR,
to avoid a conflict with the previously installed remote definition. For information about writing
an autoinstall program to control the installation of shipped definitions, see Writing a program to
control autoinstall of shipped terminals.
**NO**
When a START request is received from a terminal-owning region, and a shipped definition for the
named terminal is already installed in the AOR, the request is shipped to the TOR referenced in
the definition, for routing.
**Note:**
1. FSSTAFF has no effect:
- On statically-defined (hard-coded) remote terminal definitions in the AOR. If you use these,
START requests are always shipped to the TORs referenced in the definitions.

**70**   CICS TS for z/OS: System Initialization Parameter Reference


- On START requests issued in the local region. It affects only START requests shipped from other
    regions.
- When coded on intermediate regions in a transaction-routing path. It is effective only when
    coded on an application-owning region.
2. If the AOR contains no remote definition of a terminal named on a shipped START request, the
"terminal not known" global user exits, XICTENF and XALTENF, are called. For details of these
exits, see Terminal not known condition exits XALTENF and XICTENF.

## FTIMEOUT..................................................................................................................................................

```
The FTIMEOUT system initialization parameter specifies a timeout interval for requests made on files that
are opened in RLS mode.
FTIMEOUT={ 30 |number}
The timeout interval is in seconds, from 1 through 4080 (sixty eight minutes) and indicates how long
VSAM should wait before terminating a request and returning an exception condition.
The default is 30 seconds.
FTIMEOUT applies to transactions that do not have a deadlock timeout interval active. If a time value
is specified for the DTIMOUT keyword of the TRANSACTION definition, this value is used as the file
timeout value for that transaction.
To understand how transaction deadlocks occur, see Transaction deadlocks. You must design your
program to avoid transaction deadlocks; follow Program design: Designing to avoid transaction deadlocks
and observe the rules for avoiding deadlocks.
```
## GMTEXT......................................................................................................................................................

```
The GMTEXT system initialization parameter specifies whether the default logon message text (WELCOME
TO CICS) or your own message text is to be displayed on the screen.
GMTEXT={'DFHZC2312 *** WELCOME TO CICS ***'|'text'}
The message text can be displayed by the CSGM (good morning) transaction when a terminal is
logged on to CICS through z/OS Communications Server, by the CESN transaction if used to sign on to
CICS, or by your own transactions using the EXEC CICS INQUIRE SYSTEM GMMTEXT command.
You can use apostrophes to punctuate your message, in addition to using them as message delimiters.
However, you must code two successive apostrophes to represent a single apostrophe in your text. For
example,
```
```
GMTEXT='User''s logon message text.'
```
```
The whole message must still be enclosed by a pair of single delimiting apostrophes.
Your message text can be from 1 through 246 characters (bytes), and can extend over two lines by
extending the text to column 80 on the first line, and continuing in column 1 of the second line. For
example, for CICS Transaction Server for z/OS, Version 6 Release 2, the following might be used in the
SYSIN data set:
```
```
* CICS Transaction Server for z/OS, Version 6 Release 2 SYSTEM *
GMTEXT='A Development CICS Terminal-Owning Region (TOR) - C
ICSIDC. This message is to show the use of continuation lines when creating a GM
TEXT parameter in the SYSIN data set' (for first signon
```
```
Using the same example, the CSGM transaction displays this (with the time appended to the end of
message):
```
```
A Development CICS Terminal-Owning Region (TOR) - C
ICSIDC. This message is to show the use of continuation lines when creating a GM
TEXT parameter in the SYSIN data set 09:56:14
```
```
Chapter 1. System initialization parameter summary   71
```

```
And the CESN transaction displays this:
```
```
Signon for CICS Transaction Server for z/OS, Version 6 Release 2 APPLID CICSHTH1
A Development CICS Terminal-Owning Region (TOR) - CICSIDC.
This message is to show the use of continuation lines when creating a GMTEXT
parameter in the SYSIN data set
```
```
For any transaction other than CESN that displays the text specified by this parameter, you must use a
TYPETERM with LOGONMSG(YES) for all terminals requiring the logon message. For information about
using TYPETERM, see Autoinstalling model terminal definitions.
```
## GMTRAN.....................................................................................................................................................

```
The GMTRAN system initialization parameter specifies the ID of a transaction.
```
1. The specified transaction is automatically initiated (ATI) when terminals are logged on to CICS by z/OS
    Communications Server, and LOGONMSG(YES) is specified in the TYPETERM definition.
2. The specified transaction is set to be the next transaction initiated by the terminal operator following
    expiry of the terminal user's TIMEOUT period (specified in RACF), and either of the following attributes
    is specified in the TYPETERM definition:
    - LOGONMSG(YES) and SIGNOFF(YES)

```
or
```
- LOGONMSG(YES), SIGNOFF(LOGOFF) and DISCREQ(NO)
3. The specified transaction is automatically set to be the next transaction initiated when doing CESF
logoff.
**GMTRAN** is initiated when terminals are logged on to CICS by z/OS Communications Server.
You can specify one of CICS-supplied transactions CSGM, CESL, or CESN, or a user transaction.
**Note:** Do not specify the name of a remote transaction. The transaction must be capable of being
automatically initiated (ATI).
**GMTRAN=({CSGM|CESL|CESN|transaction-id}[,{EXIT|DISCONNECT}])
CSGM**
This is the default. CSGM displays the text specified in the **GMTEXT** parameter.
**CESL or CESN**
You can also specify one of the CICS sign-on transactions, CESL or CESN, which also displays the
text specified in the **GMTEXT** parameter.
**EXIT**
This option affects only CESN or CESL. When PF3 or PF15 is used, the sign-on transaction CESN or
CESL terminates. The terminal session is not disconnected. This is the default.
**DISCONNECT**
This option affects only CESF, CESN, or CESL.

```
Transaction Effect
```
```
CESN or CESL When PF3 or PF15 is used, the terminal
session is disconnected and the sign-on
transaction CESN or CESL terminates.
```
```
CESF The terminal session is disconnected.
```
```
The TYPETERM attribute DISCREQ is not used for the terminal at which CESF, CESN, or CESL is
used to disconnect a terminal session.
```
**72**   CICS TS for z/OS: System Initialization Parameter Reference


```
Note: The EXIT and DISCONNECT options will only be honored for CICS supplied transactions. For
user transactions, EXEC CICS ASSIGN GMEXITOPT must be called to discover which option is set
and the transaction must then implement the desired behavior.
The GMTRAN parameter can be used with the LGNMSG parameter to retrieve z/OS Communications Server
logon data.
```
```
Security considerations
When CESN or CESL is in use for terminal sign-on, you can control what happens if the user fails to
complete the sign-on, by setting the EXIT or DISCONNECT option.
When PF3 or PF15 is used, by default (EXIT) the CICS sign-on transaction terminates but the terminal
session remains connected. If the user fails to complete the sign-on, all subsequent transactions use the
CICS default user ID. This situation might compromise the terminal session security.
To allow for better terminal session security, you can specify CESN or CESL with option DISCONNECT on
GMTRAN. This setting allows terminal users to either enter with a valid sign-on credential or disconnect
the terminal session. To do the same if you specify a user transaction on GMTRAN , you should define the
user transaction to initiate CESN or CESL; otherwise, the user transaction should determine what actions
to take.
Another security advantage in using GMTRAN=(,DISCONNECT) is to ensure that when users issue CESF,
their terminal sessions are disconnected upon sign-off.
```
## GNTRAN.....................................................................................................................................................

```
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
```
```
Chapter 1. System initialization parameter summary   73
```

#### DISCARD

```
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
```
## GRNAME.....................................................................................................................................................

```
The GRNAME system initialization parameter specifies the z/OS Communications Server generic resource
name, as 1 through 8 characters, under which a group of CICS terminal-owning regions in a CICSplex
register to z/OS Communications Server.
GRNAME=name
There is no default for the GRNAME parameter. If you do not specify a value for this parameter, CICS
does not register itself with the z/OS Communications Server generic resources function.
The following restrictions apply when specifying the GRNAME parameter:
```
1. If you have a CICSPlex that comprises separate terminal-owning regions and application-owning
    regions, define a z/OS Communications Server generic resource name to the CICS terminal-owning
    regions only.
2. Generic resource names must be unique within a single network. A generic resource cannot be
    identical to:
    - A USERVAR
    - An alias name
    - A real LU name
    It is your responsibility to follow these restrictions.
3. The first character of the **GRNAME** parameter value cannot be a number.
For example, a CICS region with the system initialization parameters:

```
APPLID=CICSHTH1
GRNAME=CICSH###
```
```
registers to z/OS Communications Server with the applid CICSHTH1 and the generic resource
CICSH###. Other LUs in the same sysplex can communicate with the CICS region either through
the generic resource or the applid.
Note: If GRNAME is specified and you sign on with a PassTicket, the PassTicket must be generated
using GRNAME and not the applid.
Take care with LU6 connections initiated from this side (such as AUTOCONNECT(YES)) because the
bind contains the generic resource name and might fail if the partner knows this region only by the
applid. Binds that are initiated from the partner are examined to identify the name by which the
```
**74**   CICS TS for z/OS: System Initialization Parameter Reference


```
partner knows this region (generic resource or applid). This allows the appropriate connection to
be built. For information about defining connections, see Configuring z/OS Communications Server
generic resources.
```
## GRPLIST.....................................................................................................................................................

```
The GRPLIST system initialization parameter specifies the names of up to four lists of resource definition
groups on the CICS system definition file (CSD). The resource definitions in all the groups in the specified
lists are loaded during initialization when CICS performs a cold start. If a warm or emergency start is
performed, the resource definitions are derived from the global catalog, and the GRPLIST parameter is
ignored.
GRPLIST={DFHLIST |name|(name[,name2][,name3][,name4])}
You can specify up to four list names. A list name contains 1 - 8 characters. Each name can be either
a real group list name or a generic group list name that incorporates global filename characters (+ and
*).
The default is DFHLIST, the CICS-supplied list that specifies the set of resource definitions needed
by CICS. If you create your own group list, either add to it the groups specified in DFHLIST (omitting
only those for CICS functions that you know you do not need) or specify the DFHLIST name on the
GRPLIST parameter. Do not code GRPLIST=NO unless you have a group list named NO.
Note:
```
1. If you specify more than one group list (either by specifically coding two or more group list
    names or by coding a group list name with global filename characters), the later group lists
    are concatenated onto the first group list. Any duplicate resource definitions in later group lists
    override those in earlier group lists; however, the installation of the later resource definition fails if
    it is a resource type that requires the resource definition be disabled before it can be reinstalled.
    Examples of such resources are ATOMSERVICE, DB2ENTRY, FILE and TDQUEUE.
2. Group lists specified by a generic group list name are concatenated in alphabetic, then numeric,
    order. For example, the generic list name CICSHT* would concatenate the group lists CICSHT#1,
    CICSHTAP, CICSHTSD, and CICSHT3V in that order. If the order of concatenation is important (for
    example, to ensure that a particular resource definition overrides another), consider coding real
    group list names.
3. If a group list contains resource definitions that are needed by another group list, the group list
    containing those definitions must be installed first. For example, if list A has TYPETERM definitions
    needed for TERMINAL definitions in list B, list A must be installed first. Therefore, you might need
    to specifically name the prerequisite group on the **GRPLIST** parameter.
4. Take care when using generic group list names, because if a group list on your CSD satisfies the
    generic name, it will be installed. This means that a group list can be installed more than once; for
    example, if you specify the real group list name and a generic group list name that it satisfies, or if
    you specify two generic group list names that the group list name satisfies.
5. To override one or more of the group lists specified on the **GRPLIST** system initialization
    parameter, you must specify all list names (both real and generic) that you want to use, even if
    you are not changing the names.
In general, any required resource definitions should appear in one of the group lists specified on the
**GRPLIST** system initialization parameter.
Use the CEDA command **LOCK** to protect the lists of resource groups specified on the **GRPLIST**
parameter.
For information about resource definitions, groups, lists, and the CSD, see CICS resources.

```
Example
To use the four group lists CICSHT#1, CICSHTAP, CICSHTSD, and CICSHT3V, you could specify either of
the following system initialization parameters:
```
```
Chapter 1. System initialization parameter summary   75
```

- **Example 1:** GRPLIST=(CICSHT*)
- **Example 2:** GRPLIST=(CICSHT#1,CICSHTAP,CICSHT3V,CICSHTSD)
In the first example, the group lists are loaded in the order CICSHT#1, CICSHTAP, CICSHTSD, then
CICSHT3V. Resource definitions installed from the CICSHT3V group list override any duplicate definitions
installed by the other groups.
In the second example, the group lists are loaded in the order specified. Resource definitions installed
from the CICSHTSD group list override any duplicate definitions installed by the other groups.
If you specify GRPLIST=(CICSHT#1,CICSAP*,CICSHT3V,CICSHTSD) and you want to replace the list
CICSHT3V with the list ANOLST05, specify the override:

```
GRPLIST=(CICSHT#1,CICSAP*,ANOLST05,CICSHTSD)
```
## GTFTR.........................................................................................................................................................

```
The GTFTR system initialization parameter specifies whether CICS can use the z/OS generalized trace
facility (GTF) as a destination for trace data.
GTFTR={OFF|ON}
This parameter controls whether any of the three types of CICS trace entry are written to GTF data
sets. The three types are: CICS system trace (see the SYSTR parameter), user trace (see the USERTR
parameter), and exception trace entries (which are always made and not controlled by a system
initialization parameter).
OFF
CICS does not use GTF as a destination for CICS trace data.
ON
CICS uses GTF as a destination for CICS trace data. To use the GTF data sets for CICS trace data,
you must have started GTF with the USR option, in addition to coding GTFTR=ON.
For information about GTF, see z/OS MVS Diagnosis: Tools and Service Aids.
```
## HPO............................................................................................................................................................

```
The HPO system initialization parameter specifies whether you want to use the z/OS Communications
Server authorized path feature of the high performance option (HPO).
HPO={NO|YES}
If you code YES, the CICS type 6 SVC must be link-edited in your MVS nucleus, and defined to MVS in
an SVCPARM statement. If the SVC number is not 215 (the default), you must specify the SVC number
on the SRBSVC parameter.
If HPO=YES and HPO activation is successful, message DFHSI1600 is issued.
If HPO=YES and HPO activation is unsuccessful, message DFHSI1601 is issued and CICS terminates.
For information about installing the CICS type 6 SVC in your MVS system, and about changing the
default number, see Selecting the high-performance option.
Restriction: You cannot specify the HPO parameter in the system console.
Note: To specify HPO in the PARM parameter on an EXEC PGM=DFHSIP statement or in the SYSIN data
set, you must define necessary security authorization. See Authorizing use of HPO in PARM parameter on
EXEC PGM=DFHSIP statement or in SYSIN data set for more information.
```
**76**   CICS TS for z/OS: System Initialization Parameter Reference


## HTTPSERVERHDR......................................................................................................................................

```
The HTTPSERVERHDR system initialization parameter specifies the value (up to 64 characters) that CICS
sets in the server header of HTTP responses.
HTTPSERVERHDR={YES|NO|'value'}
Valid values are as follows:
YES
The server header is set in outgoing HTTP responses to IBM_CICS_Transaction_Server/
version (zOS) as follows:
```
#### •

```
6.2
IBM_CICS_Transaction_Server/6.2.0(zOS)
```
#### •

```
6.1
IBM_CICS_Transaction_Server/6.1.0(zOS)
NO
CICS does not add a server header to outgoing responses.
value
When you specify a value, the server header includes this value in outgoing HTTP responses.
```
## HTTPUSRAGENTHDR.................................................................................................................................

```
The HTTPUSRAGENTHDR system initialization parameter specifies the value (up to 64 characters) that
CICS sets in the user-agent header of HTTP requests.
HTTPUSRAGENTHDR={YES|NO|'value'}
Valid values are as follows:
YES
The user-agent header is set in outgoing HTTP requests to IBM_CICS_Transaction_Server/
version (zOS) as follows:
```
#### •

```
6.2
IBM_CICS_Transaction_Server/6.2.0(zOS)
```
#### •

```
6.1
IBM_CICS_Transaction_Server/6.1.0(zOS)
NO
CICS does not add a user-agent header to outgoing requests.
value
When you specify a value, the user-agent header includes this value in outgoing HTTP requests.
```
## ICP..............................................................................................................................................................

```
The ICP system initialization parameter specifies that you want to perform a cold start for interval control
program.
ICP=COLD
If COLD is not specified, the ICP start type will be determined by the START and TS parameter values.
If TS=COLD and START=AUTO is specified, then Interval Control Elements created without FROM data
will be restored on a WARM start. See Defining CICS resource table and module keywords for further
information.
The interval control program is used for time management. See Interval control for details.
```
```
Chapter 1. System initialization parameter summary   77
```

## ICV..............................................................................................................................................................

```
The ICV system initialization parameter specifies the region exit time interval in milliseconds.
ICV={ 1000 |number}
The ICV system initialization parameter specifies the maximum time in milliseconds that CICS
releases control to the operating system when there are no transactions ready to resume processing.
This time interval can be any integer in the range 100 through 3600000 milliseconds (specifying an
interval up to 60 minutes). A typical range of operation might be 100 through 2000 milliseconds.
A low value interval can enable much of the CICS nucleus to be retained in dynamic storage, and
not be paged-out at times of low terminal activity. This reduces the amount of dynamic storage
paging necessary for CICS to process terminal transactions (thus representing a potential reduction in
response time), sometimes at the expense of concurrent batch region throughput.
Large networks with high terminal activity are inclined to run CICS without a need for this value,
except to handle the occasional, but unpredictable, period of inactivity. These networks can usually
function with a large interval (10000 to 3600000 milliseconds). After a task is initiated, the system
recognizes its requests for terminal services and the completion of the services, and this maximum
delay interval is overridden.
Small systems, or those with low terminal activity, are subject to paging introduced by other jobs
running in competition with CICS. By specifying a low value interval, key portions of the CICS
nucleus are referenced more frequently, thus reducing the probability of these pages being paged-
out. However, the execution of the logic without performing productive work might be considered
wasteful. The need to increase the probability of residency by frequent but unproductive referencing
must be weighed against the overhead and response time degradation incurred by allowing the paging
to occur. By increasing the interval size, less unproductive work is performed at the expense of
performance if paging occurs during the periods of CICS activity.
For information about interval control parameters and performance, see Interval control value
parameters: ICV, ICVR, and ICVTSD.
Note: The region exit time interval process contains a mechanism to ensure that CICS does not
constantly set and cancel timers (thus degrading performance) while attempting to meet its objectives
for a low region exit time interval. This mechanism can cause CICS to release control to the operating
system for up to 0.5 seconds when the interval has been set at less than 250; and up to 0.25 seconds
more than the region exit time interval when the interval has been set greater than 250.
```
## ICVR...........................................................................................................................................................

```
The ICVR system initialization parameter specifies the default runaway task time interval in milliseconds
as a decimal number.
ICVR={ 2000 |number}
You can specify zero, or a number in the range 250 through 2 700 000, in multiples of 250. CICS
rounds down values that are not multiples of 250. This is the RUNAWAY interval used by transactions
defined with RUNAWAY=SYSTEM. See TRANSACTION resources for further information.
CICS might purge a task if it has not given up control after the RUNAWAY interval for the transaction
(or ICVR if the transaction definition specified RUNAWAY=SYSTEM). If you code ICVR=0, runaway task
control is inoperative for transactions specifying RUNAWAY=SYSTEM in their transaction definition
(that is, tasks do not get purged if they appear to be looping). The ICVR value is independent of the
ICV value, and can be less than the ICV value. CICS runaway task detection is based upon task time,
that is, the interval is decremented only when the task has control of the processor.
Important: Java uses a modified ICVR value. For more information, see CICS task and thread
management.
For information about commands that reinitialize the ICVR value, see Investigating loops that cause
transactions to abend with abend code AICA.
```
**78**   CICS TS for z/OS: System Initialization Parameter Reference


## ICVTSD.......................................................................................................................................................

```
The ICVTSD system initialization parameter specifies the terminal scan delay value.
ICVTSD={ 0 |number}
The terminal scan delay facility was used in earlier releases to limit how quickly CICS dealt with
some types of terminal output requests made by applications, in order to spread the overhead for
dealing with the requests. The range is 0 through 5000 milliseconds. Specifying a nonzero value
was sometimes appropriate where the CICS system used non-SNA networks. However, with SNA and
IPIC networks, setting ICVTSD to 0 is appropriate to provide a better response time and best virtual
storage usage.
```
## INFOCENTER..............................................................................................................................................

```
The INFOCENTER system initialization parameter specifies the location of the online IBM Documentation.
If you add this parameter to the CICSPlex SM Web User Interface (WUI) CICS startup JCL, a link labeled
Information Center is displayed on WUI views and menus. If you do not code this parameter, CICS does
not construct links to IBM Documentation.
INFOCENTER= URL
To link to the online IBM Documentation, specify its URL. For example: INFOCENTER=https://
http://www.ibm.com/docs/en/cics-ts for the IBM Documentation home page for CICS Transaction
Server for z/OS.
```
## INITPARM..................................................................................................................................................

```
The INITPARM system initialization parameter specifies parameters that are to be passed to application
programs that use the ASSIGN INITPARM command.
INITPARM=(pgmname_1='parmstring_1'[, .... ,pgmname_n='parmstring_n'])
You can use INITPARM to pass parameters to PLTPI programs to be executed in the final stages of
system initialization. The area giving access to the parameters is specified by the ASSIGN INITPARM
command. For programming information about the ASSIGN INITPARM command, see ASSIGN.
pgmname
The name of a program. This name must be 1 through 8 alphanumeric or national language
characters.
parmstring
The parameter string (up to 60 characters enclosed by single quotes) to be passed to the
associated program. Any quotes imbedded in the string must be duplicated. For information
on coding INITPARM in the SYSIN data set, see Rules for coding CICS system initialization
parameters in the SYSIN data set.
You can specify up to 255 pgmname='parmstring' sets.
Note: In SYSIN, you can specify the INITPARM keyword and its parameters more than once, see A
sample CICS startup job. If you specify INITPARM multiple times for the same program, the final
INITPARM parameter specified is the parameter that the system uses. If you specify INITPARM multiple
times for different programs, the INITPARM parameters specified are merged.
```
## INTRDRJOBUSER.......................................................................................................................................

```
6.2
Applies to 6.2.
The INTRDRJOBUSER system initialization parameter instructs whether to use the task user ID or the
CICS region user ID as the job user ID for a JOB card that is submitted, without a USER parameter, by
```
```
Chapter 1. System initialization parameter summary   79
```

```
using SPOOLOPEN with USERID("INTRDR") and SPOOLWRITE. The default is the task user ID unless set
otherwise by INTRDRJOBUSER.
INTRDRJOBUSER={TASK|REGION}
Valid values are as follows:
TASK
A job without the USER parameter, submitted by SPOOL commands to the internal reader, uses the
task user ID as the job user ID. This is the default.
REGION
A job without the USER parameter, submitted by SPOOL commands to the internal reader, uses the
CICS region user ID as the job user ID.
If the job user ID is not the task user ID and no password is supplied, it is necessary to grant the task user
ID surrogate authority to submit jobs on behalf of the job user ID. If the surrogate security check fails, the
command fails with a NOTAUTH response. In addition, a DFHXS1111 message is issued to the CICS log,
and an ICH408I message is issued to the console and job log. For details about this security, see Security
for submitting a JCL job to the internal reader.
```
## INTTR.........................................................................................................................................................

```
The INTTR system initialization parameter specifies whether the internal CICS trace destination is to be
activated at system initialization.
INTTR={ON|OFF}
This parameter controls whether any of the three types of CICS trace entry are written to the internal
trace table. The three types are CICS system trace (see the SYSTR parameter), user trace (see the
USERTR parameter), and exception trace entries (which are always made and not controlled by a
system initialization parameter).
ON
Activate main storage trace.
OFF
Do not activate main storage trace.
When CICS is running, you can change internal trace settings dynamically through the CETR transaction.
```
## IRCSTRT.....................................................................................................................................................

```
The IRCSTRT system initialization parameter specifies whether interregion communication (IRC) is to be
started up at system initialization. IRC allows connections to be established between this CICS system
and other systems, including DL/I batch regions and non-CICS client programs using the external CICS
interface (EXCI).
IRCSTRT={NO|YES}
If IRCSTRT=YES is not coded, you can start and initialize IRC by issuing a SET IRC OPEN command
or by using the CEMT SET IRC OPEN transaction.
```
## ISC..............................................................................................................................................................

```
The ISC system initialization parameter specifies whether the CICS programs required for multiregion
operation (MRO) and intersystem communication over SNA (ISC over SNA) are to be included.
ISC over SNA allows communication between CICS and non-CICS systems or CICS systems that are not
in the same z/OS image or sysplex. It can also be used between CICS regions in the same z/OS image or
sysplex. For configuration information, see Configuring support for ISC over SNA.
By using MRO, CICS systems that are running in the same z/OS image, or in the same z/OS sysplex, can
communicate with each other without the need to use a network access method such as ACF/SNA or
TCP/IP. For each CICS region that is to use MRO, you must specify ISC=YES to include the intersystem
communication program, DFHISP. For more information, see Enabling MRO for CICS startup.
```
**80**   CICS TS for z/OS: System Initialization Parameter Reference


```
For IPIC interconnectivity (IPIC), specify ISC=YES and TCPIP=YES.
ISC={NO|YES}
The values are as follows:
NO
This is the default value. The CICS programs required for MRO and ISC over SNA are not initialized.
YES
The CICS programs required for MRO and ISC over SNA are initialized.
```
## JESDI..........................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The JESDI system initialization parameter specifies, in a SIT for an alternate XRF system, the JES delay
interval.
JESDI={ 30 |number} (alternate)
The minimum is 5 seconds. The alternate CICS region has to ensure that the active CICS region has
been canceled before it can take over the resources owned by the active.
Note: You must give careful consideration to the values you specify for the parameters ADI and
JESDI so that they do not conflict with your installation's policy on PR/SM RESETTIME and the XCF
INTERVAL and OPNOTIFY intervals. You should ensure that the sum of the interval you specify for
ADI plus JESDI exceeds the interval specified by the XCF INTERVAL and the PR/SM policy interval
RESETTIME.
```
## JVMPROFILEDIR........................................................................................................................................

```
The JVMPROFILEDIR system initialization parameter specifies the name (up to 240 characters long) of a
z/OS UNIX directory that contains the JVM profiles for CICS. CICS searches this directory for the profiles it
needs to configure JVMs.
JVMPROFILEDIR={/usr/lpp/cicsts/ cicstsversion /JVMProfiles | directory }
The default value of JVMPROFILEDIR is the same as the default value of the USSHOME system
initialization parameter, which specifies the name and path of the root directory for CICS files on z/OS
UNIX, followed by the subdirectory JVMProfiles:
```
#### •

```
6.2
/usr/lpp/cicsts/cicsts62/JVMProfiles
```
#### •

```
6.1
/usr/lpp/cicsts/cicsts61/JVMProfiles
Changing the USSHOME parameter has no effect on the JVMPROFILEDIR parameter value.
If you want CICS to load the JVM profiles from a different directory, you must do one of the following:
```
- Change the value of the **JVMPROFILEDIR** system initialization parameter.
- Use UNIX soft links to link to your JVM profiles from the directory that is specified by **JVMPROFILEDIR**.
    Use this method to store your JVM profiles in any place in the z/OS UNIX file system.
For JVM servers that are defined in CICS bundles, the JVM profile is packaged in the CICS bundle along
with the JVMSERVER resource definition. CICS does not load these JVM profiles from the directory that
is specified by **JVMPROFILEDIR**. Instead, the file path is relative to the root directory of the CICS bundle.
For more information see Referencing zFS artifacts in a bundle.

```
Chapter 1. System initialization parameter summary   81
```

## KERBEROSUSER........................................................................................................................................

```
The KERBEROSUSER system initialization parameter specifies the user ID that is associated with the
Kerberos service principal for the CICS region. This parameter is optional. Specify this parameter if you
want the region to support the Kerberos service. If this parameter is not specified, the Kerberos service is
disabled in the region.
KERBEROSUSER={ kerberos_userid }
You can specify any valid user ID to be associated with the Kerberos service principal for the CICS
region.
Recommendation: The user ID associated with the Kerberos service principal for the CICS region must
not be a protected user ID. Because the CICS region user ID is protected to prevent revocation, do not use
it for the Kerberos service principal.
For information about Kerberos support in CICS, see How it works: Kerberos.
```
## KEYRING....................................................................................................................................................

```
The KEYRING system initialization parameter specifies the fully qualified name of the key ring, within
the RACF database, that contains the keys and X.509 certificates used by CICS support for the Secure
Sockets Layer (SSL) and for web services security. The region user ID that will use the key ring must either
own the key ring or have the authority to use the key ring if it is owned by a different region user ID. You
can create an initial key ring with the DFH$RING exec that is supplied in the CICSTS nn .CICS.SDFHSAMP
library, where CICSTS nn is your version of CICS. For example, for CICS Transaction Server for z/OS,
Version 6 Release 2, this is CICSTS62.CICS.SDFHSAMP.
Note:
```
- The **KEYRING** parameter is not used by Liberty JVM server's SSL support. If that is your only use of SSL
    in the CICS region, you do not have to specify the **KEYRING** parameter.
- When AT-TLS is used to secure socket sessions, CICS SSL/TLS system initialization parameters such
    as **KEYRING** , **MINTLSLEVEL** , and **MAXTLSLEVEL** are no longer required because the implementation of
    TLS is provided by AT-TLS policy statements and all encryption and decryption is done outside of the
    CICS address space. For more information, see Implementation options for TLS.
    The CICS region user ID still requires access to the key ring that is specified in the AT-TLS policy. If you
    are migrating from CICS SSL to AT-TLS, you can continue to use the existing CICS-owned key rings and
    reference them in the AT-TLS policies. If you want to set up new key rings in TCPIP, the CICS region user
    ID will require access to this new key ring. The server certificate will remain as either a CICS-owned or
    SITE certificate.
**KEYRING=** **_keyring-name_**
    The maximum length of the **KEYRING** parameter is 47 characters, and the key ring name is case-
    sensitive. The following formats are accepted as the key ring name:

```
*
Ring.Name
USERID /*
USERID / Ring.Name
*AUTH*/*
*SITE*/*
```
```
where:
*
Specifies a virtual key ring that contains all the certificates owned by the region user ID.
Ring.Name
Specifies a key ring owned by the region user ID.
USERID /*
Specifies a virtual key ring that contains all the certificates owned by the named region user ID
( USERID ).
```
**82**   CICS TS for z/OS: System Initialization Parameter Reference


```
USERID / Ring.Name
Specifies a key ring owned by the named region user ID ( USERID ).
*AUTH*/*
Specifies the system virtual key ring that contains all the CA certificates. It is useful for regions
that only use outbound connections and hence don't need individual certificates of their own.
*SITE*/*
Specifies the system virtual key ring that contains all the SITE certificates.
For more information about creating a key ring, see Building a key ring manually.
```
## LGDFINT.....................................................................................................................................................

```
The LGDFINT system initialization parameter specifies the log defer interval to be used by CICS log
manager when determining how long to delay a forced journal write request before invoking the z/OS
System Logger.
LGDFINT={ 5 | number }
The value is specified in milliseconds.
5
This is the default. When this parameter was first introduced, the default value was 30
milliseconds, but customer experience has shown that 5 is a more realistic value.
number
number can be any value in the range 0 through 65535. You are recommended to allow LGDFINT
to assume its default value, 5.
You can modify the log defer interval dynamically using the LOGDEFER option of the CEMT SET
SYSTEM or EXEC CICS SET SYSTEM command. However, you are recommended not to modify this
value in a production environment without first performing a system evaluation and performance
analysis of any changed value.
If you change the log defer interval value dynamically, the new value is not cataloged. The log defer
interval value is taken from the LGDFINT system initialization parameter in all types of CICS startup.
When a CICS system has many tasks issuing forced log write requests, these tasks will not be delayed
for periods close to the LGDFINT parameter value. This is because a forced log write request is
normally issued while a log deferral is already being performed for another task. The actual interval
might also be affected by the need for tasks to wait across a partition exit.
```
## LGNMSG.....................................................................................................................................................

```
The LGNMSG system initialization parameter specifies whether z/OS Communications Server logon data is
to be made available to an application program.
LGNMSG={NO|YES}
Valid values are as follows:
NO
z/OS Communications Server logon data is not available to an application program.
YES
z/OS Communications Server logon data is available to an application program. The data can
be retrieved with an EXEC CICS EXTRACT LOGONMSG command. For programming information
about this command, see EXTRACT LOGONMSG.
You can use this parameter with the GMTRAN parameter to retrieve the z/OS Communications
Server logon data at the time a terminal is logged on to CICS by z/OS Communications Server.
```
```
Chapter 1. System initialization parameter summary   83
```

## LLACOPY.....................................................................................................................................................

```
The LLACOPY system initialization parameter specifies the situations where CICS uses either the
LLACOPY macro or the BLDL macro when locating modules in the DFHRPL or dynamic LIBRARY
concatenation.
LLACOPY={YES|NO|NEWCOPY}
Valid values are as follows:
YES
CICS always uses the LLACOPY macro when locating modules in the DFHRPL or dynamic LIBRARY
concatenation.
NO
CICS always uses the BLDL macro when locating modules in the DFHRPL or dynamic LIBRARY
concatenation.
NEWCOPY
CICS uses the LLACOPY only when a NEWCOPY or a PHASEIN is being performed. At all other
times, CICS uses the BLDL macro when locating modules in the DFHRPL or dynamic LIBRARY
concatenation.
You can improve the performance of module fetching on your system by allowing library lookaside
(LLA) to manage your production load libraries. LLA reduces the amount of I/O needed to locate and
fetch modules from DASD storage. For more information about this, refer to Improving module fetch
performance with LLA in the z/OS MVS Initialization and Tuning Guide.
Note:
```
1. If you code LLACOPY=NO or LLACOPY=NEWCOPY you can still benefit from having LLA managed
    data sets within your DFHRPL or dynamic LIBRARY concatenation. Modules will continue to be
    loaded from the virtual lookaside facility (VLF) if appropriate. For more information about VLF and
    LLA refer to Controlling LLA and VLF through operator commands in the z/OS MVS Initialization and
    Tuning Guide.
2. If an LLA managed module has been altered, a BLDL macro may not return the new information
    and a subsequent load will still return the old copy of the module. To load the new module, an
    LLACOPY must be issued against that module or a MODIFY LLA,REFRESH command must be
    issued on a system console.
3. If you set LLACOPY to anything other than NO, ensure that the proper RACF security permissions
    have been set up first. For more information about this refer to Summary of RACF classes for CICS
    resources.
4. If an LLACOPY is issued against an LLA managed module, it creates a BLDL macro to interact with
    the specified DCB. If the directory information does not match the information stored in LLA, the
    LLA tables are updated to keep both subsystems synchronized. Whilst the LLA tables are being
    updated, SYSZLLA1.update has an enqueue (lock) held against it until LLA is stopped or the library
    is removed from LLA management.

## LOCALCCSID...............................................................................................................................................

```
The LOCALCCSID system initialization parameter specifies the default CCSID for the local region.
The LOCALCCSID parameter is used to set the default encoding for some CICS API commands. API
commands that use the LOCALCCSID are documented as such, but most APIs (for example, the
CONTAINER GET and PUT commands) do not use this parameter.
LOCALCCSID={ 037 |CCSID}
The CCSID is a value of up to 8 characters. If CCSID value is not specified, the default LOCALCCSID is
set to 037. For lists of valid CCSIDs, see the following information:
```
- CICS-supported conversions
- The relevant appendix in z/OS Unicode Services User's Guide and Reference

**84**   CICS TS for z/OS: System Initialization Parameter Reference


#### 037

```
The default value for LOCALCCSID.
CCSID
Represents any other valid EBCDIC CCSID value.
```
## LPA..............................................................................................................................................................

```
The LPA system initialization parameter specifies whether CICS and user modules can be used from the
link pack areas.
LPA={NO|YES}
Valid values are as follows:
NO
will not load CICS or user modules from the link pack areas.
YES
CICS or user modules installed in the LPA or in the ELPA can be used from there instead of being
loaded into the CICS region.
A list of the CICS modules that are read-only and, therefore eligible for residence in the link
pack areas (LPA or ELPA), is contained in a member called DFH$UMOD in the SMP/E USERMOD
that is supplied in the CICSTS nn .CICS.SDFHSAMP library, where CICSTS nn is your version
of CICS. For example, for CICS Transaction Server for z/OS, Version 6 Release 2, this is
CICSTS62.CICS.SDFHSAMP.
```
```
For details of the CICS system initialization parameter PRVMOD that you can use to override
LPA=YES for selected modules, see “PRVMOD” on page 105.
```
## MAXOPENTCBS..........................................................................................................................................

```
The MAXOPENTCBS system initialization parameter specifies the maximum number, in the range 32
through 4032, of open task control blocks (open TCBs) CICS can create in the pool of L8 and L9 mode
TCBs.
If you do not specify the MAXOPENTCBS parameter, the MXT value is used to set a value for the
MAXOPENTCBS parameter. For more information on how the value is set from MXT, see Open TCB
management.
If you must explicitly specify the MAXOPENTCBS parameter, or change its value dynamically using EXEC
CICS SET DISPATCHER , then you must set it to a correct and optimum value. If you change MXT,
however you choose to specify it (as a system initialization parameter, using CEMT or EXEC CICS SET
DISPATCHER , or using CICS Explorer®), you should review your explicit setting for MAXOPENTCBS. Be
aware that, to revert to allowing CICS to set MAXOPENTCBS automatically after you have specified it
explicitly, you must reinitialize both the local and global catalogs.
MAXOPENTCBS= number
Within this limit, there are no constraints on how many of the TCBs in the pool are L8 TCBs, and how
many are L9 TCBs.
```
- L8 mode TCBs are used in the following circumstances:
    - For CICSKEY OPENAPI application programs.
    - For OPENAPI task-related user exits (TRUEs), for example the CICS-Db2 and IBM MQ Attachment
       Facilities, and the CICS-DBCTL Database Adapter Transformer (DFHDBAT) when used with IMS
       Version 12 or later. TRUEs always run in CICSKEY.
    - By CICS itself, because CICS uses OPENAPI CICSKEY programs that run on L8 TCBs when
       accessing doc templates and HTTP static responses that are stored in z/OS UNIX System
       Services files, or when processing web service requests and parsing XML. CICS also runs some

```
Chapter 1. System initialization parameter summary   85
```

```
security requests on L8 TCBs. CICS uses L8 TCBs when authenticating a password, password
phrase or kerberos token when the original request was on the QR TCB.
```
- L9 mode TCBs are used for USERKEY OPENAPI application programs.
For more information about open TCBs, see Open TCB management.

## MAXSOCKETS.............................................................................................................................................

```
The MAXSOCKETS system initialization parameter specifies the maximum number of IP sockets that can
be managed by the CICS sockets domain.
MAXSOCKETS={65535| number }
Set a suitable value that does not exceed the maximum value as defined in the MAXFILEPROC
parameter in SYS1.PARMLIB member BPXPRMxx. If you specify a value greater than the
MAXFILEPROC parameter, CICS issues message DFHSO0124, which specifies the value that CICS
has used for this parameter. If the CICS region user ID has superuser authority, the MAXFILEPROC
parameter does not limit the setting of MAXSOCKETS.
The maximum number of sockets must be greater than the maximum number of inbound and
outbound sockets used by CICS including the number of TCPIPSERVICE resources in service.
When CICS is at the MAXSOCKETS limit and a new socket is required, CICS attempts to close the
oldest idle inbound connection to allow the new socket to be created. If there are no idle inbound
connections, then CICS closes an idle connection from an outbound connection pool. If there are no
idle outbound connections, CICS is unable to create a new socket and issues message DFHSO0126 to
report the failure.
```
## MAXSSLTCBS..............................................................................................................................................

```
CICS uses the open transaction environment (OTE) to manage SSL connections and requests to LDAP
using the DFHDDAPX XPI interface. Each SSL connection uses an S8 TCB from the SSL pool. The
MAXSSLTCBS system initialization parameter specifies the maximum number of S8 TCBs that can run
in the SSL pool.
A CICS region limits the number of concurrent TLS handshakes to 90% of the MAXSSLTCBS value
specified at startup. If the number of concurrent TLS handshakes reaches the maximum limit, a task
that is requesting a TLS handshake is suspended with a resource name of S8TLSHS.
MAXSSLTCBS={ 32 | number }
The default is 32, but you can specify between 1 and 1024 TCBs.
This value must not exceed the MAXTHREADS and MAXTHREADTASKS parameter values, which are
specified in SYS1.PARMLIB member BPXPRMxx.
For more information about open TCBs, see Open TCB management.
```
## MAXTLSLEVEL............................................................................................................................................

```
The MAXTLSLEVEL system initialization parameter specifies the maximum TLS protocol that CICS uses for
secure TCP/IP connections.
Note: When AT-TLS is used to secure socket sessions, CICS SSL/TLS system initialization parameters
such as KEYRING , MINTLSLEVEL and MAXTLSLEVEL are no longer required because the implementation
of TLS is provided by AT-TLS policy statements and all encryption and decryption is done outside of the
CICS address space. For details, see Implementation options for TLS.
MAXTLSLEVEL={TLS11|TLS12|TLS13}
When a secure connection is established between a pair of processes, the most secure TLS protocol
that is supported by both processes is used.
TLS11
Sets the maximum level of TLS to 1.1.
```
**86**   CICS TS for z/OS: System Initialization Parameter Reference


#### TLS12

```
Sets the maximum level of TLS to 1.2. This is the default value.
TLS13
Sets the maximum level of TLS to 1.3.
```
```
6.1
```
```
Restriction:
6.1
Sysplex caching by using the SYSPLEX option is not supported for TLS 1.3.
```
## MAXXPTCBS...............................................................................................................................................

```
The MAXXPTCBS system initialization parameter specifies the maximum number, in the range 1 through
2000, of open X8 and X9 TCBs that can exist concurrently in the CICS region.
If you do not specify the MAXXPTCBS parameter, the MXT value will be used to set a value for
the MAXXPTCBS parameter. For more information on how the value is set from MXT, see Open TCB
management.
If you must explicitly specify the MAXXPTCBS parameter, or change its value dynamically using EXEC
CICS SET DISPATCHER , then you must set it to a correct and optimum value. If you change MXT,
however you choose to specify it (as a system initialization parameter, using CEMT, or EXEC CICS SET
DISPATCHER, or using CICS Explorer) you should review your explicit setting for MAXXPTCBS. Be aware
that, to revert to allowing CICS to set MAXXPTCBS automatically after specifying it explicitly, you must
reinitialize both the local and global catalogs.
MAXXPTCBS= number
X8 and X9 are the TCBs that are used to provide support for C and C++ programs compiled with the
XPLINK option.
For more information about open TCBs, see Open TCB management.
```
## MCT............................................................................................................................................................

```
The MCT system initialization parameter specifies the monitoring control table suffix.
MCT={NO|YES|xx}
Valid values are as follows:
NO
is the default and causes the CICS monitoring domain to dynamically build a default monitoring
control table. This ensures that default monitoring control table entries are always available for
use when monitoring is on and a monitoring class (or classes) are active. You can generate an
MCT with a single-character suffix only for use by CICS because single-character suffixes cause
an error when the MCT is processed by DFHMNDUP. If you use DFHMNDUP, make sure that you
create your MCTs with two-character suffixes.
For information about coding the macros for this table, see Generating a performance dictionary
record using DFHMNDUP.
YES
CICS will load DFHMCT.
xx
CICS will load DFHMCTxx.
```
```
Chapter 1. System initialization parameter summary   87
```

## MINTLSLEVEL.............................................................................................................................................

```
The MINTLSLEVEL system initialization parameter specifies the minimum TLS protocol that CICS uses for
secure TCP/IP connections.
Note: When AT-TLS is used to secure socket sessions, CICS SSL/TLS system initialization parameters
such as KEYRING , MINTLSLEVEL , and MAXTLSLEVEL are no longer required because the implementation
of TLS is provided by AT-TLS policy statements and all encryption and decryption is done outside of the
CICS address space. For more information, see Implementation options for TLS.
MINTLSLEVEL={TLS11|TLS12|TLS13}
When a secure connection is established between a pair of processes, the most secure TLS protocol
that is supported by both processes is used.
TLS11
Sets the minimum level of TLS to 1.1.
TLS12
Sets the minimum level of TLS to 1.2. This setting is the default value.
TLS13
Sets the minimum level of TLS to 1.3.
```
```
Changing minimum TLS protocol levels
If you are looking to raise the minimum TLS protocol level that is defined in MINTLSLEVEL , you want to be
certain to identify all handshakes that are made by using that protocol. For more information about how to
manage the process, see Changing TLS protocol level or ciphers safely.
```
**FIPS 140-2 standards**

```
To apply FIPS 140-2 standards, set MINTLSLEVEL =TLS12 and NISTSP800131A =CHECK.
If NISTSP800131A =CHECK is set but MINTLSLEVEL is set to TLS11, it is overridden to
MINTLSLEVEL =TLS12 and a warning message is issued. This check does not apply if TLS is set to 1.3.
To apply FIPS 140-2 standards on z/OS Version 2 Release 1 or later, ICSF (Integrated Cryptographic
Services Facility) must be active on your system.
For more information about NIST SP800-131A conformance, see Making your CICS TS system
conformant to NIST SP800-131A.
```
## MN..............................................................................................................................................................

```
The MN system initialization parameter specifies whether monitoring is to be switched on or off at
initialization.
MN={OFF|ON}
Use the individual monitoring class system initialization parameters to control which monitoring
classes are to be active (see the MNEXC, MNPER, and MNRES parameter descriptions.) The default
status is that the CICS monitoring facility is off. The monitoring status is recorded in the CICS global
catalog for use during warm and emergency restarts.
OFF
Switch off monitoring.
ON
Turn on monitoring. However, unless at least one individual class is active, no monitoring records
are written.
Note:
```
1. If the monitoring status is ON, CICS accumulates monitoring data continuously. For each
    monitoring class that is active, CICS writes the monitoring data to a system management facilities

**88**   CICS TS for z/OS: System Initialization Parameter Reference


```
(SMF) data set. If the monitoring status is OFF, CICS does not accumulate or write any monitoring
data, even if any of the monitoring classes are active.
```
2. You can change the monitoring status and the monitoring class settings at any time, as follows:
    - During a warm restart by coding system initialization parameters in PARM, SYSIN, or through the
       system console.
    - While CICS is running, by using the monitoring facility transaction CEMN, the **CEMT SET**
       **MONITOR** command, or the **EXEC CICS SET MONITOR** command.
    When you change the status of monitoring, the change takes effect immediately. If you change
    the monitoring status from OFF to ON, monitoring starts to accumulate data and write monitoring
    records to SMF for all tasks that start after the status change is made, for all active monitoring
    classes. If the status is changed from ON to OFF, monitoring stops writing records immediately and
    does not accumulate monitoring data for any tasks that start after the status change is made.
3. The monitoring status setting can be manipulated independently of the class settings. This means
    that, even if the monitoring status is OFF, you can change the monitoring class settings, and the
    changes take effect for all tasks that are started after the monitoring status is next set to ON.

## MNCONV.....................................................................................................................................................

```
The MNCONV system initialization parameter specifies whether conversational tasks have separate
performance class records produced for each pair of terminal control I/O requests.
MNCONV={NO|YES}
Any clock (including user-defined) that is active at the time such a performance class record is
produced is stopped immediately before the record is written. After the record is written, such a
clock is reset to zero and restarted. Thus a clock whose activity spans more than one recording
interval within the conversational task appears in multiple records, each showing part of the time, and
the parts add up to the total time that the clock is active. The high watermark fields (which record
maximum levels of storage used) are reset to their current values. All other fields are set to X'00',
except for the key fields (transid, termid). The monitoring converse status is recorded in the CICS
global catalog for use during warm and emergency restarts.
```
## MNEXC........................................................................................................................................................

```
The MNEXC system initialization parameter specifies whether the monitoring exception class is to be made
active during initialization.
MNEXC={OFF|ON}
The monitoring exception class status is recorded in the CICS global catalog for use during warm and
emergency restarts.
OFF
Set the exception monitoring class to "not active".
ON
Set the exception monitoring class to "active".
For programming information about exception monitoring records, see The schedule flag word.
```
## MNFREQ.....................................................................................................................................................

```
The MNFREQ system initialization parameter specifies the interval for which CICS automatically produces
a transaction performance class record for any long-running transaction.
The monitoring frequency value is recorded in the CICS global catalog for use during warm and
emergency restarts. CICS can produce a performance class monitoring record in this way only when
the long-running transaction is running on the QR or CO TCBs.
MNFREQ={ 0 |hhmmss}
The values are as follows:
```
```
Chapter 1. System initialization parameter summary   89
```

#### 0

```
No frequency monitoring is active.
hhmmss
The interval for which monitoring produces automatically a transaction performance class record
for any long-running transaction. Specify a 1 to 6 digit number in the range 000100–240000.
Numbers that are fewer than six digits are padded with leading zeroes.
```
## MNIDN........................................................................................................................................................

```
The MNIDN system initialization parameter specifies whether the monitoring identity class is to be made
active during CICS initialization.
MNIDN={OFF|ON}
The monitoring identity class status is recorded in the CICS global catalog for use during warm and
emergency restarts.
OFF
Set identity monitoring class to not active.
ON
Set identity monitoring class to active.
```
## MNPER........................................................................................................................................................

```
The MNPER system initialization parameter specifies whether the monitoring performance class is to be
made active during CICS initialization.
MNPER={OFF|ON}
The monitoring performance class status is recorded in the CICS global catalog for use during warm
and emergency restarts.
OFF
Set the performance monitoring class to "not active".
ON
Set the performance monitoring class to active.
For programming information about performance monitoring records, see CICS monitoring facility:
Performance and tuning.
```
## MNRES........................................................................................................................................................

```
The MNRES system initialization parameter specifies whether transaction resource monitoring is to be
made active during CICS initialization.
MNRES={OFF|ON}
The transaction resource monitoring class status is recorded in the CICS global catalog for use during
warm and emergency restarts.
OFF
Set transaction resource monitoring to not active.
ON
Set transaction resource monitoring to active.
Transaction resource monitoring applies to CICS file resources when you specify the FILE= nn option
on the DFHMCT TYPE=INTIAL macro.
```
**90**   CICS TS for z/OS: System Initialization Parameter Reference


## MNSYNC.....................................................................................................................................................

```
The MNSYNC system initialization parameter specifies whether you want CICS to produce a transaction
performance class record when a transaction takes an implicit or explicit syncpoint (unit-of-work).
MNSYNC={NO|YES}
No action is taken for syncpoint rollbacks. The monitoring syncpoint status is recorded in the CICS
global catalog for use during warm and emergency restarts.
```
## MNTIME......................................................................................................................................................

```
The MNTIME system initialization parameter specifies whether you want the time stamp fields in the
performance class monitoring data to be returned to an application using the EXEC CICS COLLECT
STATISTICS MONITOR(taskno) command in either GMT or local time.
MNTIME={GMT|LOCAL}
The monitoring time value is recorded in the CICS global catalog for use during warm and emergency
restarts.
For programming information on the EXEC CICS COLLECT STATISTICS command, see COLLECT
STATISTICS.
The TIME option is displayed in the CEMN monitoring facility transaction, but cannot be changed through
CEMN.
```
## MQCONN....................................................................................................................................................

```
The MQCONN system initialization parameter specifies whether you want CICS to start a connection to IBM
MQ automatically during initialization.
MQCONN={NO|YES}
NO
Do not automatically call DFHMQCOD, the CICS-MQ adapter program, during initialization.
YES
Call the CICS-MQ adapter program, DFHMQCOD, automatically during CICS initialization. The
MQCONN parameter always uses program DFHMQCOD to start the CICS-MQ connection. It cannot
be customized to use a user-supplied attach program of a different name.
When you specify MQCONN=YES , the information that CICS needs to start the connection to IBM
MQ, such as the name of an IBM MQ queue manager or queue-sharing group, is taken from the
MQCONN resource definition for the CICS region.
An MQCONN resource definition must be installed before CICS can start the connection to IBM
MQ. When you start the connection automatically at CICS initialization, for an initial or cold start,
the MQCONN resource definition must be present in one of the groups named in the list or lists
named by the GRPLIST system initialization parameter. For a warm or emergency start of CICS,
the MQCONN resource definition must have been installed by the end of the previous CICS run.
When you specify MQCONN=YES , you do not need to define the CICS-MQ adapter program in the
CICS post initialization program list table (PLT).
```
## MROBTCH...................................................................................................................................................

```
The MROBTCH system initialization parameter specifies the number of events that must occur before CICS
is posted for dispatch because of the batching mechanism.
MROBTCH={ 1 |number}
The number can be in the range 1 through 255, and the default is 1.
Use this batching mechanism to spread the overhead of dispatching CICS over several tasks. If the
value is greater than 1 and CICS is in a system wait, CICS is not posted for dispatch until the specified
```
```
Chapter 1. System initialization parameter summary   91
```

```
number of events has occurred. Events include MRO requests from connected systems or DASD I/O
and CHANGE_MODE processing. For these events, CICS is dispatched as soon as one of the following
occurs:
```
- The current batch fills up (the number of events equals MROBTCH).
- An ICV interval expires.
Therefore, ensure that the time interval you specify in the ICV parameter is low enough to prevent
undue delay to the system.
If CICS is dispatched for another reason, the current batch is dealt with in that dispatch of CICS.
**Note:** During periods of low utilization, a value of MROBTCH greater than 1 might cause increased
transaction response times. Transactions that issue file I/O requests might be delayed because of
increased FCIOWAIT value. For more information about the effect of MROBTCH on performance, see
Batching requests (MROBTCH).

## MROFSE......................................................................................................................................................

```
The MROFSE system initialization parameter specifies whether you want to extend the lifetime of the
long-running mirror to keep it allocated until the end of the task rather than after a user syncpoint for
function shipping applications.
MROFSE={NO|YES}
Valid values are as follows:
NO
The lifetime of the MRO long-running mirror is not extended.
YES
The mirror task remains available to the application until the end of the application's task. This
extended long-running mirror saves the overhead of re-attaching the mirror task following a user
syncpoint.
This parameter is ignored for DPL requests (that is a DPL causes the session to be freed at the
next syncpoint even if is has been kept for a previous sequence of syncpoints).
It should be used with caution especially if DPL requests with SYNCONRETURN or TRANSID are
used. For additional information, see Long-running mirror tasks for MRO
Do not specify this value in the front-end region when long running tasks might be used to
function-ship requests. This because a SEND session is unavailable for allocation to other tasks
when unused. Specifying MROFSE=YES could prevent the connection from being released when
contact has been lost with the back-end region, until the task terminates or issues a function-
shipped request.
```
## MROLRM.....................................................................................................................................................

```
The MROLRM system initialization parameter specifies whether you want to establish an MRO long-running
mirror task.
MROLRM={NO|YES}
Valid values are as follows:
NO
The MRO long-running mirror task is not required.
YES
The mirror transaction remains available to the application issuing the remote request. This long-
running mirror saves the overhead of re-establishing communication with the mirror transaction if
the application makes more function shipping requests in this unit of work.
For information about long-running mirror tasks, see Long-running mirror tasks for MRO.
```
**92**   CICS TS for z/OS: System Initialization Parameter Reference


```
Note: The MROLRM system initialization parameter can have a significant effect on the performance
of a workload in an MRO function shipping environment. For details, see Extending the life of mirror
transactions (MROLRM and MROFSE).
```
## MSGCASE...................................................................................................................................................

```
The MSGCASE system initialization parameter specifies how you want the message domains to display
mixed case messages.
MSGCASE={MIXED|UPPER}
Messages handled by the CICS message domain and the CICSPlex SM message domain are in mixed
case.
MIXED
This is the default in the SIT; all messages displayed by the CICS message domain or the CICSPlex
SM message domain remain in mixed case.
UPPER
The message domain displays all mixed case messages in uppercase only.
Mixed case output is not displayed correctly on Katakana display terminals and printers. Uppercase
English characters appear correctly as uppercase English characters, but lowercase appears as
Katakana symbols. If you have any Katakana terminals connected to your CICS region, specify
MSGCASE=UPPER.
If you want to use uppercase English for your CICS-MQ components, you must set MSGCASE=UPPER,
and ensure that ASSIGN NATLANGINUSE returns E (US English).
```
## MSGLVL......................................................................................................................................................

```
The MSGLVL system initialization parameter specifies the message level that controls the generation of
messages to the console and JES message log.
MSGLVL={ 1 |0}
Valid values are as follows:
1
All messages are printed or displayed.
0
Only critical errors or interactive messages are printed or displayed.
For more information about how you can suppress or reroute console messages, see Console device
messages.
```
## MXT............................................................................................................................................................

```
The MXT system initialization parameter specifies the maximum number, in the range 10 through 2000, of
user tasks that can exist in a CICS system at the same time. The MXT value does not include CICS system
tasks.
MXT={ 250 |number}
CICS queues requests for tasks above this number but does not action (attach) them until the number
of tasks attached drops below the MXT limit. See Setting the maximum task specification (MXT).
Review the size specified on the z/OS REGION and MEMLIMIT parameters for the CICS address space.
The increase in CICS use of virtual storage above 16 MB but below 2 GB (above the line) means that
you probably need to increase the REGION parameter. The increase in CICS use of virtual storage
above 2 GB (above the bar) means that you probably need to increase the MEMLIMIT parameter. See
Setting the limits for CICS storage.
For CICS regions that operate with transaction isolation, the transaction isolation facility increases the
allocation of some virtual storage above 16 MB but below 2 GB.
```
```
Chapter 1. System initialization parameter summary   93
```

- If the CICS region operates with transaction isolation, CICS allocates storage for task-lifetime
    storage in multiples of 1 MB for user-key tasks that run above 16 MB but below 2 GB. 1 MB is
    the minimum unit of storage allocation for the extended user dynamic storage area (EUDSA) when
    transaction isolation is active. However, although storage above 16 MB but below 2 GB is allocated
    in multiples of 1 MB, MVS paging activity affects only the storage that is used (referenced), and
    unused parts of the 1 MB allocation are not paged.
- If the CICS region operates without transaction isolation, CICS allocates user-key task-lifetime
    storage above 16 MB but below 2 GB in multiples of 64 KB.
The subspace group facility uses more real storage, because MVS creates a page and segment table
from real storage for each subspace. The CICS requirement for real storage varies depending on the
transaction load at any one time. As a guideline, each task in the system requires 9 KB of real storage,
and this should be multiplied by the number of concurrent tasks that can be in the system at any one
time (governed by the MXT system initialization parameter).
**Note:** If the MAXOPENTCBS or MAXXPTCBS system initialization parameters have not been specified,
then setting MXT will affect the MAXOPENTCBS and MAXXPTCBS settings.
For more information about open TCBs, see Open TCB management.
**Important:** Before you change the **MXT** system initialization parameter, review the information in
Open TCB pools.
**Note:** From CICS Transaction Server for z/OS, Version 5 Release 4, tasks that are internally initiated in
a MAS by CICSPlex SM no longer execute as user tasks. As a result these tasks no longer qualify under
the MXT and transaction class limits.

## NATLANG....................................................................................................................................................

```
The NATLANG system initialization parameter specifies the single-character code for the language to be
supported in this CICS run.
NATLANG=(E|C|K)
Valid code values are as follows:
E
English, which is the system default (that is, is provided even if you do not specifically code E).
C
Simplified Chinese, a Double-Byte Character Set language. Translation is performed by IBM.
K
Japanese, a Double-Byte Character Set language. Translation is performed by IBM.
English language support is provided, even if you do not specifically code E for English.
Globalization is not available to CICS console messages, which continue to be in English only.
```
## NCPLDFT....................................................................................................................................................

```
The NCPLDFT system initialization parameter specifies the name of the default named counter pool to be
used by the CICS region on calls it makes to a named counter server.
NCPLDFT={DFHNC001|name}
If CICS cannot determine, from the named counter options table, the pool name required by an EXEC
CICS named counter command, CICS uses the default name specified on the NCPLDFT parameter.
Note: This parameter is relevant to references to a named counter server made through the EXEC
CICS API only. It not used by the named counter call interface.
DFHNC001
This is the default name that CICS uses as the named counter pool name if you omit the NCPLDFT
system initialization parameter.
```
**94**   CICS TS for z/OS: System Initialization Parameter Reference


```
name
Specifies the 8-character name to be used by CICS as the default pool name in connection with
named counter API commands, when the name cannot be resolved by the named counter options
table.
```
## NEWSIT......................................................................................................................................................

```
The NEWSIT system initialization parameter specifies whether CICS is to load the specified SIT, and
enforce the use of all system initialization parameters, modified by any system initialization parameters
provided by PARM, SYSIN, or the system console, even in a warm start.
NEWSIT={YES|NO}
Enforcing the use of system initialization parameters in this way overrides any parameters that may
have been stored in a warm keypoint at shutdown.
However, there are some exceptions. The following system initialization parameters are always
ignored in a warm start, even if they are supplied by PARM, SYSIN, or the console:
```
- CSDACC
- CSDBUFND
- CSDBUFNI
- CSDDISP
- CSDDSN
- CSDFRLOG
- CSDINTEG
- CSDJID
- CSDLSRNO
- CSDRECOV
- CSDRLS
- CSDSTRNO
- FCT
- GRPLIST
In a warm restart, CICS uses the **installed** resource definitions saved in the CICS global catalog at
warm shutdown, and therefore the CSD, FCT, and GRPLIST parameters are ignored. (At CICS startup,
you can only modify installed resource definitions, including file control table entries, or change to a
new FCT, by performing a cold start of CICS with START=COLD.)
For more information about the use of the NEWSIT parameter, see Controlling start and restart.
**Restriction:** You can specify the NEWSIT parameter in PARM, SYSIN, or CONSOLE only.

## NISTSP800131A........................................................................................................................................

```
The NISTSP800131A system initialization parameter specifies whether the CICS region is to check for
conformance to the NIST SP800-131A standard.
Note: This is ignored if MAXTLSLEVEL is set to TLS13.
NISTSP800131A={NOCHECK|CHECK}
NOCHECK
Conformance checking is not required in this CICS region. This is the default value.
CHECK
The CICS region is required to check for conformance with the NIST SP800-131A security
standard. If this value is set, CICS issues a message if an actual or potential violation is detected.
```
```
Chapter 1. System initialization parameter summary   95
```

```
This option also causes the CICS SSL environment to use only TLS version 1.2 with FIPS 140-2
standards applied.
The checks that are performed are as follows:
Web services
If the <wsse_handler> tag is specified in a pipeline configuration file, it implies that the
pipeline is to be used for web services security. Because not all of the encryption algorithms
that can be used for web services security conform to SP800-131A, installing a pipeline
that uses web services means that CICS might be non-conformant. CICS issues message
DFHXS1300, which warns of potential nonconformance.
If you receive message DFHXS1300, check whether you are using DFHWSSE as the web
services security handler. If you are not using DFHWSSE, inspect your security handler to
check which encryption and signing algorithms it uses. If these algorithms are SP800-131A
conformant, you can ignore the message. If they are not conformant, consider whether to use
conformant algorithms instead. Otherwise, if the CICS region that issues the message must
be conformant, consider moving the web service security workload to a different CICS region
where conformance is not required.
CICS also checks for certain things that are not conformant to SP800-131A. If any of these
situations are found, CICS issues message DFHXS1301:
```
- An <algorithm> element exists within the <authentication> element of the <wsse_handler>
    definition in the pipeline configuration file. The only algorithms that can be used are SHA-1
    routines, which are not conformant with NIST SP800-131A.
- A <sign_body> element exists in the pipeline configuration file. The only algorithms that can
    be used are SHA-1 routines, which are not conformant with SP800-131A.
- An <encrypt_body> element in the pipeline configuration file. Of the four algorithms that
    can be used, three are conformant with SP800-131A but one is not. If the nonconformant
    algorithm is specified, DFHXS1301 is issued.
If you receive message DFHXS1301, consider not performing the encryption or signing
operations in this CICS region. If the nonconformant algorithm is specified in the
<encrypt_body> element, consider using a conformant algorithm.
**Sockets**
If SSL is active, setting **NISTSP800131A** =CHECK forces **MINTLSLEVEL** =TLS12 if it is not
already set. If **MINTLSLEVEL** =TLS12 is forced, message DFHSO0144 is issued. Sockets
domain initializes the SSL environment with the FIPS option on and the System SSL started
task runs in FIPS mode. The effect of this is that SSL allows fewer ciphers to be used on a
successful handshake.
To use FIPS with z/OS Version 2 Release 1 or later, ICSF (Integrated Cryptographic Services
Facility) must be active on your system.
If SSL is inactive because no **KEYRING** parameter is specified, then setting NISTSP800131A
has no effect on sockets domain.
**JVM servers**
When a JVM server is started, CICS sets the Java properties to make Java NIST SP800-131A
conformant.
If you set **NISTSP800131A** =CHECK, you should also set **MINTLSLEVEL** =TLS12. However, if you do
not do so, CICS overrides the value of **MINTLSLEVEL** to **MINTLSLEVEL** =TLS12 and issues a warning
message.

## NONRLSRECOV..........................................................................................................................................

```
The NONRLSRECOV system initialization parameter specifies whether VSAM catalog recovery options
should override those specified on the CICS FILE resource definition for all non-RLS files. Default
```
**96**   CICS TS for z/OS: System Initialization Parameter Reference


```
behavior, with NONRLSRECOV=VSAMCAT , will take recovery attributes from the catalog if they are present,
and from the file definition otherwise. RLS files must always specify recovery options on the catalog.
To open a data set in non-RLS mode, ensure that NONRLSRECOV=FILEDEF , and alternative recovery
attributes will be used.
Where VSAM log replication is being used, this parameter must be set to NONRLSRECOV=VSAMCAT.
NONRLSRECOV={VSAMCAT|FILEDEF}
Recovery options do not apply to read-only files. Valid values are as follows:
VSAMCAT
By default, CICS uses the recovery options that are specified on the VSAM catalog for non-RLS
files. These recovery options include the LOG, LOGSTREAMID, and BWO options. If no recovery
options are set, CICS uses the attributes on the FILE resource.
FILEDEF
For non-RLS files, CICS ignores any recovery options on the catalog and uses the values specified
in the FILE resource instead. The recovery attributes for the CSD are set by the appropriate system
initialization parameters. This option is not compatible with the LOGREPLICATE option, which can
only be specified on the VSAM catalog.
```
## NQRNL........................................................................................................................................................

```
The NQRNL system initialization parameter controls resource name list (RNL) processing by z/OS global
resource serialization, which can cause the scope value of a resource to change. CICS uses z/OS global
resource serialization to provide sysplex-wide protection of application resources.
NQRNL={NO|YES}
For more information on global resource serialization and RNL processing, see z/OS MVS Planning:
Global Resource Serialization.
Valid values are as follows:
NO
NO is the default value in CICS. When NQRNL=NO is specified, the sysplex-wide EXEC CICS ENQ
and EXEC CICS DEQ commands use the RNL=NO parameter on the z/OS ENQ or DEQ requests.
Use NQRNL=NO when you are sure that you want the request to be processed only by z/OS global
resource serialization using only the scope specified in the ENQMODEL resource definition in CICS.
When NQRNL=NO is specified, the sysplex-wide EXEC CICS ENQ and EXEC CICS DEQ requests
are ignored by alternative serialization products.
YES
When NQRNL=YES is specified, the sysplex-wide EXEC CICS ENQ and EXEC CICS DEQ
commands use the RNL=YES parameter on the z/OS ENQ or DEQ requests. This parameter allows
z/OS global resource serialization to perform RNL processing, searching an appropriate RNL to
determine the scope of the resource. This setting is the default in z/OS.
For more information on using ENQMODEL definitions in CICS to specify the scope for resources, see
ENQMODEL resources.
```
## OFFSITE.....................................................................................................................................................

```
The OFFSITE system initialization parameter specifies whether CICS is to restart in off-site recovery
mode; that is, a restart is taking place at a remote site.
OFFSITE={NO|YES}
For a successful off-site restart, the log records of the failed CICS region must be available at the
remote site. CICS does not provide a facility for shipping log records to a remote backup site, but you
can use a suitable vendor product to perform this function. See the relevant product documentation
for other procedures you need to follow for a remote site restart.
See Administering restart and recovery for more information about remote site recovery.
```
```
Chapter 1. System initialization parameter summary   97
```

#### NO

```
CICS will not perform the special restart processing required for remote site recovery.
YES
CICS will perform an off-site restart at a remote site following a disaster at the primary site. CICS
performs this special processing for an off-site restart, because some information (for example, a
VSAM lock structure) is not available at the remote site.
CICS performs an emergency restart, even if the global catalog indicates that CICS can do a warm
start. OFFSITE=YES is valid with START=AUTO only, and CICS initialization is terminated if you
specify START=COLD or INITIAL.
Restriction: You can specify the OFFSITE parameter in PARM, SYSIN, or CONSOLE only.
```
## OPERTIM....................................................................................................................................................

```
The OPERTIM system initialization parameter specifies the write-to-operator timeout value, in the range 0
through 86400 seconds (24 hours).
OPERTIM={ 120 |number}
This is the maximum time in seconds that CICS waits for a reply before returning control to this
transaction. You can change the write-to-operator timeout value when issuing messages to the
console from an application by using the timeout option on the WRITE OPERATOR command. See
WRITE OPERATOR for details.
```
## OPNDLIM....................................................................................................................................................

```
The OPNDLIM system initialization parameter specifies the open destination and close destination
request limit. (Not required for currently supported releases of z/OS Communications Server.)
OPNDLIM={ 10 |number}
This limit is used to restrict the number of concurrent OPNDSTs and CLSDSTs to prevent the z/OS
Communications Server from running out of space in the CICS region. The limit may be any value in
the range 0 through 999. When large values are used for OPNDLIM, the value on the EDSALIM system
initialization parameter and the value on the z/OS REGION parameter may need to be adjusted to
ensure that enough operating system storage is available.
```
## PARMERR...................................................................................................................................................

```
The PARMERR system initialization parameter specifies what action you want to follow if CICS detects
incorrect system initialization parameter overrides during initialization.
PARMERR={INTERACT|IGNORE|ABEND}
When specified as an override, this parameter affects only subsequent system initialization parameter
overrides. Errors in earlier system initialization parameter overrides are dealt with according to the
PARMERR system initialization parameter value in the SIT.
INTERACT
Enables the operator to communicate with CICS through the console and correct parameter
errors.
Note: INTERACT is overridden with IGNORE in the following cases:
```
- If errors are found in PARM or SYSIN for system initialization parameter overrides that are not
    allowed to be entered from the console
- In certain circumstances, in response to invalid data when you have been trying to correct a
    previous invalid system initialization parameter keyword or value
**IGNORE**
CICS ignores errors, and tries to complete initialization.
**ABEND**
CICS abends.

**98**   CICS TS for z/OS: System Initialization Parameter Reference


## PCDSASZE..................................................................................................................................................

```
The PCDSASZE parameter specifies the size of the PCDSA dynamic storage area. Message DFHSM0136I
at initialization shows the value that is set.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
PCDSASZE={ 0 | number }
Valid values are as follows:
0 (zero)
The size of the PCDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the PCDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes
(256 KB).
If the value you specify is not a multiple of 256 KB, CICS rounds up the value to the next
multiple.You can specify number as a number of bytes, a whole number of kilobytes, or a whole
number of megabytes. Use the letter M to indicate that the value represents a whole number
of megabytes (for example, 4 M). Use the letter K to indicate that the value represents a whole
number of kilobytes (for example, 4096 K), in which case the number is rounded up to the number
of megabytes.
Restriction: You can specify the PCDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## PDI..............................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The PDI system initialization parameter specifies the XRF primary delay interval, in seconds, in a SIT for
an active CICS region.
PDI={ 30 |decimal-value}
The minimum delay that you can specify is 5 seconds. This is the time that must elapse between the
(apparent) loss of the surveillance signal in the alternate CICS region, and any reaction by the active
CICS region. The corresponding parameter for the alternate CICS region is ADI. PDI and ADI need not
have the same value.
```
## PDIR...........................................................................................................................................................

```
The PDIR system initialization parameter specifies a suffix for the PDIR list.
PDIR={NO|YES|xx}
A PDIR is a list of program specification blocks (PSBs) that define, for DL/I, the use of databases by
application programs. A PDIR is applicable only if you are using DL/I remote support. Specifying a
value other than NO implies to CICS that remote DLI support is required.
For information about coding the macros for this table, see Defining resources with macros.
```
```
Chapter 1. System initialization parameter summary   99
```

## PGAICTLG................................................................................................................................................

```
The PGAICTLG system initialization parameter specifies whether autoinstalled program definitions should
be cataloged.
PGAICTLG={MODIFY|NONE|ALL}
While CICS is running, you can set dynamically whether autoinstalled programs should be cataloged,
by using either the EXEC CICS SET SYSTEM or CEMT SET SYSTEM command.
The setting that you specify for cataloging of autoinstalled programs has no effect on programs that
are autoinstalled by a task for an application that is deployed on a platform. These programs are never
cataloged.
MODIFY
Autoinstalled program definitions are cataloged only if the program definition is modified by a SET
PROGRAM command subsequent to the autoinstall.
NONE
Autoinstalled program definitions are not cataloged. This gives a faster CICS restart (warm
and emergency) compared with the MODIFY or ALL options, because CICS does not reinstall
definitions from the global catalog. Definitions are autoinstalled on first reference.
ALL
Autoinstalled program definitions are written to the global catalog at the time of the autoinstall,
and following any subsequent modification.
```
## PGAIEXIT.................................................................................................................................................

```
The PGAIEXIT system initialization parameter specifies the name of the program autoinstall exit
program.
PGAIEXIT={DFHPGADX|name}
The default program autoinstall exit program is DFHPGADX.
While CICS is running, you can set the name of the program autoinstall exit program dynamically, by
using either the EXEC CICS SET SYSTEM or CEMT SET SYSTEM command.
For programming information about how to write a program to control autoinstall of programs, see Writing
a program to control autoinstall of programs.
```
## PGAIPGM.................................................................................................................................................

```
The PGAIPGM system initialization parameter specifies the state of the program autoinstall function at
initialization. You can autoinstall programs, mapsets, and partitionsets. If the autoinstall program function
is enabled, when an implicit or explicit load request is issued for a previously undefined program, mapset,
or partitionset, CICS dynamically creates a definition, and installs and catalogs it, as appropriate.
PGAIPGM={INACTIVE|ACTIVE}
While CICS is running, you can set the status of program autoinstall dynamically, by using either IBM
CICS Explorer or the CICSPlex SM Web User Interface.
INACTIVE
The program autoinstall function is disabled.
ACTIVE
The program autoinstall function is enabled.
```
**100**   CICS TS for z/OS: System Initialization Parameter Reference


## PGCHAIN..................................................................................................................................................

```
The PGCHAIN system initialization parameter specifies the character string that is identified by terminal
control as a BMS terminal page-chaining command.
PGCHAIN=character(s)
The character string can be 1 through 7 characters. For more information about the character string,
see “PGRET” on page 101.
```
## PGCOPY....................................................................................................................................................

```
The PGCOPY system initialization parameter specifies the character string that is identified by terminal
control as a BMS command to copy output from one terminal to another.
PGCOPY=character(s)
The character string can be 1 through 7 characters. For more information about the character string,
see “PGRET” on page 101.
```
## PGPURGE.................................................................................................................................................

```
The PGPURGE system initialization parameter specifies the character string that is identified by terminal
control as a BMS terminal page-purge command.
PGPURGE=character(s)
It can be 1 through 7 characters. For more information about the character string, see “PGRET” on
page 101.
```
## PGRET......................................................................................................................................................

```
The PGRET system initialization parameter specifies the character string that is recognized by terminal
control as a BMS terminal page-retrieval command.
PGRET=character(s)
The character string can be 1 through 7 characters.
```
1. Each character string is unique with respect to the leading characters of every other transaction
    identification defined in the CSD. A command requested by a single character precludes the use of
    all other transaction identifications starting with this character.
2. In pseudoconversational mode, each character string is unique with respect to the leading
    characters of any terminal input message.
3. A field-separator or other suitable delimiter may be specified in each character string to separate
    this command code from the remainder of the paging command when entered by an operator. For
    example:

```
PGCHAIN = X/
PGCOPY = C/
PGPURGE = T/
PGRET = P/
```
```
This reduces the risk of creating a nonunique command. (See Note 1.)
Restriction:
If you specify PGCHAIN, PGCOPY, PGPURGE, or PGRET in the SIT, the characters you choose must
not include any of the following: ( ) '
If you specify PGCHAIN, PGCOPY, PGPURGE, or PGRET as a PARM, SYSIN, or console parameter,
do not enclose the characters in quotation marks. The characters you choose must not include an
embedded blank or any of the following: ( ) ' =
```
4. PGCHAIN, PGCOPY, PGPURGE, and PGRET are required only if full function BMS is being used. For
    information about the BMS page retrieval transaction CSPG, see CSPG - page retrieval.

```
Chapter 1. System initialization parameter summary   101
```

5. CICS always processes a paging command entered by the operator before initiating a transaction
    invoked by an **EXEC CICS RETURN** command with the TRANSID option.

## PLTPI........................................................................................................................................................

```
The PLTPI system initialization parameter specifies the suffix for, or the full name of, a program list table
that contains a list of programs to be run in the final stages of system initialization.
PLTPI={NO| name |YES}
If NO is specified, no program list table is used.
If name is one or two characters (and not NO), the characters are suffixed at the end of the DFHPLT
prefix.
If name is three to eight characters in length (and not YES), it specifies the full name of the program
list table.
If YES is specified, a table called DFHPLT (without any suffix) is used.
For information about coding the macros for the program list table, see Program list table (PLT).
For information about writing initialization programs, see Writing initialization programs. You can use
the INITPARM system initialization parameter to pass parameters to those programs.
```
## PLTPISEC.................................................................................................................................................

```
The PLTPISEC system initialization parameter specifies whether you want CICS to perform command
security or resource security checking for PLT programs during CICS initialization.
PLTPISEC={NONE|CMDSEC|RESSEC|ALL}
The PLT programs run under the authority of the userid specified on PLTPIUSR, which must be
authorized to the appropriate resources defined by PLTPISEC.
NONE
You do not want any security checking on PLT initialization programs.
CMDSEC
You want CICS to perform command security checking only.
RESSEC
You want CICS to perform resource security checking only.
ALL
You want CICS to perform both command and resource security checking.
Restriction: You can specify the PLTPISEC parameter in the SIT, PARM, or SYSIN only.
```
## PLTPIUSR.................................................................................................................................................

```
The PLTPIUSR system initialization parameter specifies the user ID that CICS uses for security checking
for PLT programs that run during CICS initialization.
PLTPIUSR= userid
All PLT programs run under the authority of the specified user ID, which must be authorized to all the
resources referenced by the programs, as defined by the PLTPISEC parameter.
PLT programs are run under the CICS internal transaction, CPLT. Before the CPLT transaction is
attached, CICS performs a surrogate user check against the CICS region userid (the userid under
which the CICS region is executing). This is to ensure that the CICS region is authorized as a surrogate
for the userid specified on the PLTPIUSR parameter. This ensures that you cannot arbitrarily specify
any PLT userid in any CICS region; each PLT userid must first be authorized to the appropriate CICS
region.
If you do not specify the PLTPIUSR parameter, CICS runs PLTPI programs under the authority of the
CICS region userid, in which case CICS does not perform a surrogate user check. However, the CICS
region userid must be authorized to all the resources referenced by the PLT programs.
```
**102**   CICS TS for z/OS: System Initialization Parameter Reference


```
Restriction: You can specify the PLTPIUSR parameter in the SIT, PARM, or SYSIN only.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
Related information
Surrogate security
```
## PLTSD.......................................................................................................................................................

```
The PLTSD system initialization parameter specifies the suffix for, or full name of, a program list table that
contains a list of programs to be run during system termination.
PLTSD={NO| name |YES}
If NO is specified, no program list table is used.
If name is one or two characters (and not NO), the characters are suffixed at the end of the DFHPLT
prefix.
If name is three to eight characters in length (and not YES), it specifies the full name of the program
list table.
If YES is specified, a table called DFHPLT (without any suffix) is used.
See Defining CICS resource table and module keywords.
```
## PRGDLAY..................................................................................................................................................

```
The PRGDLAY system initialization parameter specifies the BMS purge delay time interval that is added to
the specified delivery time to determine when a message is to be considered undeliverable and therefore
purged.
PRGDLAY={ 0 |hhmm}
This time interval is specified in the form hhmm (where hh represents hours from 00 to 99 and mm
represents minutes from 00 to 59). If PRGDLAY is not coded, or is given a zero value, a message
remains eligible for delivery either until it is purged or until there is a cold start of temporary storage.
Note: If you specify PRGDLAY as a SIT override, you must still specify a 4-character value (for
example 0000).
The PRGDLAY facility requires the use of full function BMS. Note also that you must code a PRGDLAY
value if you want the ERRTERM|ERRTERM(name) parameter on EXEC CICS ROUTE commands to be
operative.
The PRGDLAY value determines the interval between terminal page clean-up operations. A very low
value causes the CSPQ transaction to be initiated continuously, and can have a detrimental effect
on task-related resources. A zero value stops CSPQ initiating terminal page clean-up. However, this
can cause messages to stay in the system forever, resulting in performance problems with long AID
queues or lack of temporary storage. The actual purge delay time interval specified is dependent on
individual system requirements.
```
## PRINT.......................................................................................................................................................

```
The PRINT system initialization parameter specifies the method of requesting printout of the contents of
a 3270 screen.
PRINT={NO|YES|PA1|PA2|PA3}
Valid values are as follows:
```
```
Chapter 1. System initialization parameter summary   103
```

#### NO

```
Screen copying is not required.
YES
Screen copying can be requested by terminal control print requests only.
PA1, PA2, or PA3
Screen copying can be requested by terminal control print request, or by using the PA (program
attention) key specified.
The PA key specified by this parameter must not be specified by the TASKREQ option of the RDO
TRANSACTION definition or be used for 3270 single keystroke retrieval.
When YES, PA1, PA2, or PA3 is specified, transaction CSPP is initiated which invokes program
DFHP3270. The transaction and programs are defined in the CSD group DFHHARDC. In the case
of 3270 and LUTYPE2 logical units, the resources defined in CSD group DFHVTAMP are required.
The 3270 print-request facility allows either the application program or the terminal operator to
request a printout of data currently displayed on the 3270 display.
If CSPP is invoked to print the screen contents at an associated z/OS Communications Server printer,
the screen size of the printer is chosen according to the screen size defined in the profile for the
transaction CSPP. The CICS-supplied definitions use the default screen size. Therefore, if you want
DFHP3270 to use the alternate screen size of the printer, you must alter the screen size defined
in the profile for the transaction CSPP. For information about defining profiles for transactions, see
TRANSACTION resources.
For a z/OS Communications Server 3270 display without the printer-adapter feature, the PRINT
request prints the contents of the display on the first available 3270 printer specified by PRINTER and
ALTPRINTER options of the RDO TERMINAL definition. For a printer to be considered available, it must
be in service and not currently attached to a task. It is not necessary for the printer to be on the same
control unit.
In an MRO environment, the printer must be owned by the same system as the z/OS Communications
Server 3270 display.
For the 3275 with the printer-adapter feature, the PRINT request prints the data currently in the 3275
display buffer on the 3284 Model 3 printer attached to the 3275.
The format of the print operation depends on the size of the display buffer. For a 40-character wide
display, the print format is a 40-byte line, and for an 80-character wide display the format is an
80-byte line.
For the 3270 compatibility mode logical unit of the 3790 (if the logical unit has the printer-adapter
feature specified), the PRINT request prints the contents of the display on the first printer available to
the 3790. The allocation of the printer to be used is under the control of the 3790.
For 3274, 3276, and LUTYPE2 logical units with the printer-adapter feature, the PRINT request prints
the contents of the display on the first printer available to the 3270 control unit. The printer to be
allocated depends on the printer authorization matrix.
For the 3270 compatibility mode logical unit without the printer-adapter feature, see the preceding
paragraph on z/OS Communications Server 3270 displays without the printer-adapter feature.
```
## PRTYAGE..................................................................................................................................................

```
The PRTYAGE system initialization parameter specifies the number of milliseconds to be used in the
priority aging algorithm that is used to increment the priority of a task. The PRTYAGE value determines the
rate at which tasks in the system have their priorities aged. The priority aging factor is used to increase
the effective priority of a task according to the amount of time it is held on a ready queue. Adjusting the
PRTYAGE value does not control the priorities of tasks, only how CICS sets the priorities of tasks. Altering
the PRTYAGE value affects the rate at which tasks are dispatched.
PRTYAGE={ 1000 |value}
The value can be in the range 0 through 65535, and 1000 is the default.
```
**104**   CICS TS for z/OS: System Initialization Parameter Reference


```
The value represents the number of milliseconds that must elapse before the priority of a waiting task
can be adjusted upwards by 1. For example, if you code PRTYAGE=3000, a task has its priority raised
by 1 for every 3000 milliseconds it is held on the ready queue. Thus a high value for PRTYAGE results
in a task being promoted very slowly up the priority increment range, and a low value enables a task to
have its priority incremented quickly.
If you specify a value of 0, the priority aging algorithm is not used (task priorities are not modified by
age) and tasks on the ready queue are handled according to the user assigned priority.
```
## PRVMOD...................................................................................................................................................

```
The PRVMOD system initialization parameter specifies the names of those modules that are not to be used
from the link pack area (LPA).
PRVMOD={name|(name,name...name)}
The operand is a list of 1- to 8-character module names. This enables you to use a private version
of a CICS nucleus module in the CICS address space, and not a version that might be in the LPA. For
information about PRVMOD , see Using modules from DFHRPL.
Restriction: You can specify the PRVMOD parameter in PARM, SYSIN, or CONSOLE only.
```
## PSBCHK....................................................................................................................................................

```
The PSBCHK system initialization parameter specifies whether CICS is to perform PSB authorization
checks for remote terminal users who use transaction routing to initiate a transaction in this CICS region
to access an attached IMS system.
PSBCHK={NO|YES}
Valid values are as follows:
NO
The remote link is checked, but no check is made against the remote terminal. This value is the
default.
YES
The remote link is checked, and the remote terminal is also checked if RESSEC(YES) is coded in
the definition of the transaction in the CSD.
Note: If you require DL/I security checking, you must specify the XPSB system initialization parameter
as XPSB=YES or XSPB=name. For further information about the XPSB system initialization parameter,
see XPSB.
Restriction: You can specify the PSBCHK parameter in the SIT, PARM, or SYSIN only.
```
## PSDINT.....................................................................................................................................................

```
The PSDINT system initialization parameter specifies the persistent session delay interval, which states if,
and for how long, z/OS Communications Server holds sessions in a recovery-pending state.
PSDINT={0|hhmmss}
0
If a failure occurs, z/OS Communications Server sessions are terminated. Zero is the default, and
means that persistent sessions support is not exploited.
hhmmss
The time for which z/OS Communications Server retains sessions if a failure occurs, from 1 second
up to the maximum of 23 hours 59 minutes and 59 seconds. Specify a 1 to 6-digit time in hours,
minutes, and seconds. If you specify fewer than six digits, CICS pads the value with leading zeros.
Thus, a value of 500 is taken as 5 minutes exactly.
You can override this value while CICS is running. Overriding the value changes the action taken by
z/OS Communications Server if a failure occurs. The changed interval is not stored in the CICS global
catalog, and therefore is not restored in an emergency restart.
```
```
Chapter 1. System initialization parameter summary   105
```

```
z/OS Communications Server holds all sessions in a recovery-pending state for up to the interval
specified, unless they are unbound through path failure or z/OS Communications Server operator
action, or other-system action in the case of intelligent LUs. The interval you specify must be able to
cover the time from a CICS failure to the time when the z/OS Communications Server ACB is opened
by CICS during a subsequent emergency restart.
```
- If you specify SNPS (the default) or MNPS for the **PSTYPE** system initialization parameter for the
    CICS region, set a nonzero value for the persistent session delay interval, so that sessions are
    retained.
- If you specify NOPS (no persistent sessions support) for the **PSTYPE** system initialization parameter,
    a zero value is required for the persistent session delay interval.
When choosing your **PSDINT** value, take account of the types and numbers of sessions involved. You
must exercise care when specifying large **PSDINT** values because of the problems such a value might
give in some environments, in particular:
- Dial up sessions, for which real costs might be incurred.
- LU6.2 sessions to other host systems. If these sessions are retained in recovery pending state, the
    other host systems might experience excessive queuing delays. This point applies to LU6.1 sessions
    that are retained until restart, when they are unbound.

## PSTYPE.....................................................................................................................................................

```
The PSTYPE system initialization parameter specifies whether CICS uses z/OS Communications Server
single-node persistent sessions (SNPS), multinode persistent sessions (MNPS), or does not use z/OS
Communications Server persistent sessions support (NOPS).
PSTYPE={SNPS|MNPS|NOPS}
The default setting, SNPS (single-node persistent sessions), means that persistent sessions support
is available, so that z/OS Communications Server sessions can be recovered after a CICS failure
and restart. MNPS (multinode persistent sessions) means that, in addition to the SNPS support, z/OS
Communications Server sessions can also be recovered after a z/OS Communications Server or z/OS
failure in a sysplex (across LPARs).
For single-node persistent sessions support, you require z/OS Communications Server V3.4.1 or
later, which supports persistent LU-LU sessions. CICS TS for z/OS, Version 6 functions with releases
of z/OS Communications Server earlier than V3.4.1, but in the earlier releases sessions are not
retained in a bound state if CICS fails. For multinode persistent sessions support, you require z/OS
Communications Server V4.R4 or later, and z/OS Communications Server must be in a Parallel
Sysplex® with a coupling facility.
If you specify SNPS or MNPS, set a nonzero value for the PSDINT system initialization parameter,
which specifies the retention time for session information. The default is zero, which means that
sessions are not retained.
If you do not require persistent sessions support, specify NOPS. A CICS region that is used only for
development or testing might not require this support. Removing persistent sessions support where
it is not required reduces resource consumption, and can enable you to increase the number of CICS
regions in an LPAR. If you specify NOPS, a zero value is required for the PSDINT system initialization
parameter.
```
## PUDSASZE................................................................................................................................................

```
The PUDSASZE parameter specifies the size of the PUDSA dynamic storage area. Message DFHSM0136I
at initialization shows the value that is set.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
```
**106**   CICS TS for z/OS: System Initialization Parameter Reference


```
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
PUDSASZE={ 0 | number }
Valid values are as follows:
0 (zero)
Specifies that the size of the PUDSA dynamic storage area size can change dynamically. Zero is the
default.
number
A non-zero value specifies that the size of the PUDSA dynamic storage area is fixed. Specify
number as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes
(256 KB). If the value you specify is not a multiple of 256 KB, CICS rounds up the value to the next
multiple..
You can specify number as a number of bytes, a whole number of kilobytes, or a whole number of
megabytes. Use the letter M to indicate that the value represents a whole number of megabytes
(for example, 4 M). Use the letter K to indicate that the value represents a whole number of
kilobytes (for example, 4096 K), in which case the number is rounded up to the number of
megabytes.
Restriction: You can specify the PUDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## PVDELAY..................................................................................................................................................

```
The PVDELAY system initialization parameter specifies the persistent verification delay as a value in the
range 0 through 10080 minutes (up to 7 days).
PVDELAY={ 30 |number}
PVDELAY defines how long entries can remain in the signed-on-from lists for those connections
for which persistent verification is specified in a connection resource definition. If you specify
PVDELAY=0, entries are deleted immediately after use.
Tip: The ISC/IRC attach time statistics of the DFHSTUP listing is for a CICS system using intersystem
communication or interregion communication. It provides summary statistics for the number of times that
the entries on the Persistent Verification "signed on from" list are either reused or timed out. Using this
data you can adjust the USRDELAY and PVDELAY system initialization parameters. For more information,
see ISC/IRC attach time entry statistics.
```
## QUIESTIM................................................................................................................................................

```
The QUIESTIM system initialization parameter specifies a timeout value for data set quiesce requests.
QUIESTIM={ 240 |number}
In a busy CICSplex, it is possible for the default timeout to expire before the quiesce request has been
processed by all the CICS regions, even though there is nothing wrong. If the quiesce operation is not
completed when the timeout period expires, SMS VSAM cancels the quiesce. If you find that timeout
is occurring too frequently, increase the timeout value.
Specify the timeout value as a number of seconds. The default value is 240 seconds (4 minutes)
The maximum timeout value you can specify is 3600 (1 hour).
```
## RACFSYNC...............................................................................................................................................

```
The RACFSYNC system initialization parameter specifies whether CICS listens for type 71 ENF events and
refreshes user security.
Note: Specify the RACFSYNC=NO parameter only under direction from IBM Service.
```
```
Chapter 1. System initialization parameter summary   107
```

```
RACF sends a type 71 ENF signal to listeners when a CONNECT , REMOVE , or REVOKE command changes
a user's resource authorization, or when a user ID is revoked automatically as a result of too many failed
password attempts.
When CICS receives a type 71 ENF event for a user ID, all cached user tokens for the user ID are
invalidated, irrespective of the setting of the USRDELAY parameter. Subsequent requests from that user
ID force a full RACF RACROUTE VERIFY request, which results in a refresh of the user's authorization
level. User tokens for tasks that are currently running are not affected. User tokens for signed-on users
are not affected, but subsequent work in other regions will be.
CICS also makes Db2 threads for the associated user ID issue a full sign-on when they are next reused.
```
```
6.2
CICSPlex SM can also process type 71 ENF events for a CICSplex. You must specify
RACFSYNC=YES , or use the default, for the CMAS region and specify RACFSYNC=CPSM for the MAS regions
under control of the CMAS. This configuration enables the CMAS to listen for and process type 71 ENF
events and its connected MAS regions to obtain type 71 ENF event data directly from the CMAS. When
the CMAS region receives a type 71 ENF event, security information for the affected user ID is rebuilt the
next time the user ID is used, irrespective of the setting of the SECTIMEOUT parameter. The MAS regions
process type 71 ENF events in the same way as CICS.
RACFSYNC={YES|NO|CPSM}
Valid values are as follows:
YES
CICS listens for type 71 ENF events.
```
```
6.2
A CMAS listens for and processes type 71 ENF events, and makes type 71 ENF event data
available in CICSPlex SM storage for its connected MAS regions to consume.
NO
CICS does not listen for type 71 ENF events.
```
```
6.2
CPSM
A MAS does not register as a type 71 ENF event listener but obtains type 71 ENF event data
directly from its owning CMAS. The MAS attempts to obtain data from the CMAS every 15 seconds.
RACFSYNC=CPSM is intended only for a MAS region. If RACFSYNC=CPSM is specified for a CMAS,
message EYUCI0103E is issued.
Note:
```
- In the configuration where type 71 signals are issued for large numbers of users simultaneously,
    combined with large numbers of connections to Db2, the temporary performance overhead might be
    significant when the full sign-on processing across all affected Db2 threads is completed. To reduce the
    impact of type 71 ENF processing, it is recommended that updates to large numbers of RACF users be
    made during off-peak periods.
- Support for issuing a type 71 ENF as a result of too many failed password attempts requires RACF APAR
    OA58677 and SAF APAR OA58678.
**Restriction:** You can specify the **RACFSYNC** parameter only in the system initialization table (SIT), the
**PARM** parameter of the **EXEC PGM=DFHSIP** statement, or the SYSIN data set.

## RAMAX.....................................................................................................................................................

```
The RAMAX system initialization parameter specifies the size in bytes of the I/O area allocated for each
RECEIVE ANY issued by CICS, in the range 0 through 32767 bytes.
RAMAX={ 256 |number}
If you are using APPC, do not code a value less than 256; otherwise, the results are unpredictable.
For information about coding this parameter, see Setting the size of the receive-any input areas.
```
**108**   CICS TS for z/OS: System Initialization Parameter Reference


## RAPOOL....................................................................................................................................................

```
The RAPOOL system initialization parameter specifies the number of concurrent receive-any requests that
CICS is to process from the z/OS Communications Server for SNA.
RAPOOL={ 50 |value1|(value1,value2,FORCE)}
value1 is the number of fixed request parameter lists (RPLs), receive any control elements (RACEs),
and receive any input areas (RAIAs) that are to be generated whether or not CICS uses the high
performance option (HPO). value1 , in the range 1 through 999, is also the number that are active in a
non-HPO system; value2 , in the range 0 through 999, is the number that are active in an HPO system.
The default for value1 in the DFHSIT macro is 50. The default for value2 is calculated from value1 as
follows:
If value1 = 1, value2 = 1
If value1 ≤ 5, value2 = (value1 minus 1)
If value1 ≥ 6 and ≤ 50, value2 = 5
If value1 > 50, value2 is 10 per cent of value1
Note: Code value1 equal to or greater than value2 ; if you code value1 less than value2 , CICS forces
value2 equal to value1.
If you omit the RAPOOL parameter altogether, RAPOOL=(50,5) is assumed. CICS maintains n z/OS
Communications Server RECEIVE ANYs, where n is either the RAPOOL "number active" value, or the
MXT value minus the number of active tasks, whichever is the smaller. For example, in a non-HPO
system:
If RAPOOL=2, MXT=50, active tasks = 45, then RECEIVE ANY = 2
If RAPOOL=10, MXT=50, active tasks = 45, then RECEIVE ANY = 5
If RAPOOL=10, MXT=50, active tasks = 35, then RECEIVE ANY = 10
In an HPO system:
If RAPOOL=(20,10), MXT=50, active tasks = 45, then RECEIVE ANY = 5
FORCE tells CICS to free up Receive_Any_RPLs if they are stalled. CICS decides that the
Receive_Any_RPLs are stalled if all the RA RPLs have been posted but the TCTTE for each one is
waiting for a response from a z/OS Communications Server terminal or session for 10 dispatches of
the TCP (CSTP) task.
This typically happens only if a protocol error has occurred, and sessions are waiting for a response;
for example, to a BID SHUTD request from CICS.
Each session is unbound, the Receive_Any data is lost and the RA RPL is reissued thus allowing z/OS
Communications Server activity to continue: Message DFHZC4949 is issued for each session affected.
Consider increasing the size of the RAPOOL before resorting to the use of FORCE.
If FORCE is not specified and a Receive_Any stall occurs, DFHZC2118 is written to the console for
each session affected.
If FORCE is specified in the SIT, and RAPOOL is supplied as an override, you must again specify FORCE
as otherwise it defaults to FORCE not specified.
The number of RECEIVE ANYs needed depends on the expected activity of the system, the average
transaction lifetime, and the MAXTASK value specified. For information about coding this parameter,
see the Setting the size of the receive-any pool.
```
## RDSASZE..................................................................................................................................................

```
The RDSASZE system initialization parameter specifies the size of the RDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
```
```
Chapter 1. System initialization parameter summary   109
```

```
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
RDSASZE={0K|number}
Valid values are as follows:
0 (zero)
The size of the RDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the RDSA dynamic storage area is fixed. Specify number
as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes (256 KB).
If the value you specify is not a multiple of 256 KB, CICS rounds up the value to the next multiple.
You can specify number as a number of bytes, a whole number of kilobytes, or a whole number of
megabytes. Use the letter M to indicate that the value represents a whole number of megabytes
(for example, 4 M). Use the letter K to indicate that the value represents a whole number of
kilobytes (for example, 4096 K), in which case the number is rounded up to the number of
megabytes.
Restriction: You can specify the RDSAZSE parameter in PARM, SYSIN, or CONSOLE only.
```
## RENTPGM.................................................................................................................................................

```
The RENTPGM system initialization parameter specifies whether you want CICS to allocate the read-only
DSAs from read-only key-0 protected storage.
For information about the CICS DSAs, see CICS dynamic storage areas (DSAs).
RENTPGM={PROTECT|NOPROTECT}
The permitted values are PROTECT (the default), or NOPROTECT:
PROTECT
CICS obtains the storage for the read-only DSAs from key-0 protected storage.
NOPROTECT
CICS obtains the storage from CICS-key storage, effectively creating two more CICS DSAs. This
allows programs eligible for the read-only DSAs to be modified by programs that execute in CICS
key.
In production CICS regions, RENTPGM=PROTECT provides the correct level of protection for modules
in the read-only DSAs. Specifying RENTPGM=NOPROTECT is only appropriate for development
regions.
For more information, see Storage protection.
```
## RESOVERRIDES.......................................................................................................................................

```
The RESOVERRIDES system initialization parameter specifies the 1-64 character name of the resource
overrides file.
RESOVERRIDES= name
There is no default for the RESOVERRIDES parameter. If you do not specify a value for this parameter,
the resource definition overrides feature is not enabled.
file_name is the name of the resource overrides file that you want to create, for example
resourceoverrides.yaml.
```
- The file extension must be .yaml or .yml.
- The maximum length of the file name, including the file extension, is 64 characters.
- You cannot specify a subdirectory by including a backslash character (/) in the file name.
- The resource overrides file will be located in the _ussconfig_ /resourceoverrides directory,
    where _ussconfig_ is the location that is specified by the **USSCONFIG** system initialization parameter,

**110**   CICS TS for z/OS: System Initialization Parameter Reference


```
for example /var/cicsts/dfhconfig/resourceoverrides. (Message DFHPA2002I in the
system message log shows the path of the ussconfig /resourceoverrides directory for your
CICS region.) The maximum length of the total path and file name must not be greater than 310
characters.
For more information, see How it works: Resource definition overrides.
```
## RESP.........................................................................................................................................................

```
The RESP system initialization parameter specifies the type of request that CICS terminal control receives
from logical units.
RESP={FME|RRN}
Valid values are as follows:
FME
Function management end is the default.
RRN
Reached recovery node.
For information about communication with logical units, see Terminal control using SNA.
```
## RESSEC....................................................................................................................................................

```
The RESSEC system initialization parameter specifies whether you want CICS to honor the RESSEC option
specified on a transaction's resource definition.
RESSEC={ASIS|ALWAYS}
Valid values are as follows:
ASIS
CICS honors the RESSEC option defined in a transaction's resource definition. CICS calls its
resource security checking routine only when RESSEC(YES) is specified in a transaction resource
definition. This is normally a sufficient level of control, because often you will need only to control
the ability to execute a transaction.
ALWAYS
CICS overrides the RESSEC option, and always calls its resource security checking routine to issue
the appropriate call to the SAF interface.
Use this option only if you need to control or audit all accesses to CICS resources. Using this
option can significantly degrade performance.
Restriction: You can specify the RESSEC parameter in the SIT, PARM, or SYSIN only.
```
## RLS...........................................................................................................................................................

```
The RLS system initialization parameter specifies whether CICS is to support VSAM record-level sharing
(RLS). RLS is an access mode for VSAM data sets. RLS enables VSAM data to be shared, with full update
capability, between many applications running in many CICS regions. With RLS, CICS regions that share
VSAM data sets can reside in one or more z/OS images within a z/OS parallel sysplex.
RLS={NO|YES}
Valid values are as follows:
NO
RLS support is not required in this CICS region. Files whose definitions specify RLSACCESS(YES)
will fail to open, with an error indicating that RLS access is not supported. You should not specify
RLS=NO if you have files that you want to open in RLS access mode (including the CSD).
YES
RLS support is required in this CICS region. During initialization, CICS automatically registers with
an SMSVSAM control ACB to enable RLS access to files opened with RLSACCESS(YES).
```
```
Chapter 1. System initialization parameter summary   111
```

## RLSTOLSR................................................................................................................................................

```
The RLSTOLSR system initialization parameter specifies whether CICS is to include files that are to be
opened in RLS mode when calculating the number of buffers, strings, and other resources for an LSR pool.
RLSTOLSR={NO|YES}
CICS performs this calculation only when you have not explicitly defined an LSRPOOL resource
definition that corresponds to an LSRPOOLNUM in a file definition. CICS calculates and builds a
default LSR pool only when it is opening the first file in LSR mode that references the default pool.
NO
CICS is not to include files opened in RLS mode, and which also specify an LSRPOOLNUM, when
it is building default LSR pools. Files defined with RLSACCESS(YES) are ignored when CICS is
scanning file entries looking for files that specify an LSR pool it is about to build using default
values.
If the LSR pools referenced by LSRPOOLNUMs in your file resource definitions are defined
explicitly by LSRPOOL resource definitions, you must specify RLSTOLSR=NO.
YES
CICS is to include in its calculation, when building default LSR pools, files that specify both
RLSACCESS(YES) and an LSRPOOLNUM.
Note that an LSR pool built including files that are opened in RLS mode is larger than necessary
initially. This option is provided to ensure that, if files are later switched to LSR, the LSR pool
is adequate for the extra files. You should specify RLSTOLSR=YES only if both of the following
conditions are true:
```
- You do not define LSR pools explicitly, relying instead on CICS obtaining a default set of values
    for you.
- You have files that are sometimes accessed in RLS mode and sometimes accessed in non-RLS
    mode (although this is not advised).
The RLSTOLSR parameter is provided to support files that are normally opened in RLS mode, but
which can be closed and then switched to LSR mode.
If LSR pools are not defined explicitly using LSRPOOL resource definitions, CICS calculates the
resources needed for an LSR pool using default attributes. CICS performs this calculation when
opening the first file that specifies an LSR pool that is not explicitly defined. To calculate a default LSR
pool, CICS scans all the file entries to count all the files that specify the same LSRPOOLNUM. The size
of an LSR pool built dynamically in this way remains fixed until all files that reference the LSR pool are
closed. After all files have been closed, another request to open a file with the same LSRPOOLNUM
causes CICS to recalculate the size.
If you add files to the system _after_ the LSR calculation has been performed there may be insufficient
storage available to enable CICS to open a file that specifies a default pool. This situation could occur
if files are opened initially in RLS mode and later closed and reopened in LSR mode. There are two
ways to ensure that enough resources are built into the LSR pool to support subsequent switches of
files from RLS to LSR:
- You can explicitly define LSRPOOL resource definitions that correspond to the LSRPOOLNUMs on file
definitions, removing the need for CICS to calculate default values.
- You can specify RLSTOLSR=YES to force CICS to include RLS files when calculating defaults.

## RMTRAN...................................................................................................................................................

```
The RMTRAN system initialization parameter specifies the name of the transaction that you want an
alternate CICS to initiate when logged-on class 1 terminals, which are defined with the attribute
RECOVNOTIFY(TRANSACTION) specified, are switched following a takeover.
RMTRAN=({CSGM|name1}[,{CSGM |name2}])
This parameter is applicable only on an alternate CICS region.
```
**112**   CICS TS for z/OS: System Initialization Parameter Reference


```
If you do not specify a name here, CICS uses the CSGM transaction, the default CICS good morning
transaction.
name1
This is the transaction that CICS initiates at terminals that do not remain signed-on after the
takeover (that is, they are still connected to CICS, but are signed off).
name2
This is the transaction that CICS initiates at terminals that remain signed-on after the takeover. If
you specify only name1, CICS uses the CSGM transaction as the default for name2.
If you are using z/OS Communications Server persistent sessions, the name2 transaction is ignored
and the name1 transaction is always initiated.
```
## RRMS........................................................................................................................................................

```
The RRMS system initialization parameter specifies whether CICS is to register as a resource manager
with recoverable resource management services (RRMS). RRMS is part of the z/OS operating system
and comprises registration services, context services, and recoverable resource services (RRS). RRMS
provides the context and unit of recovery management.
You can use RRMS to coordinate distributed program link (DPL) requests. For details, see Use of RRMS
with the external CICS interface.
RRMS={NO|YES}
Valid values are as follows:
NO
You do not require RRMS support.
YES
You require RRMS support to enable DPL requests to be coordinated by resource recovery
services (RRS).
Note: If you specify RRMS=YES, ensure that the DFHRXSVC module is available during CICS
initialization. This module, which provides RRMS authorized services, is supplied in the SDFHLINK
library. For information about this link list library, see CICS- and CICSPlex SM-supplied modules
required in the MVS linklist.
```
## RST...........................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The RST system initialization parameter specifies a recoverable service table suffix.
The recoverable service table (RST) is used for CICS DBCTL XRF (extended recovery facility) support.
It contains a description of the DBCTL configuration. On detection of a DBCTL failure, the active CICS
system uses the RST together with the z/OS subsystem VERIFY to determine the existence of a suitable
alternative DBCTL subsystem. The alternate CICS system uses the RST to check for the presence of a
DBCTL subsystem.
RST={NO|xx|YES}
If you are running CICS with XRF=YES, and you are using DBCTL, you must specify an RST if you want
XRF support for DBCTL.
For information about coding the macros for this table, see Recoverable service table (RST).
```
```
Chapter 1. System initialization parameter summary   113
```

## RSTSIGNOFF............................................................................................................................................

```
The RSTSIGNOFF system initialization parameter specifies whether all users signed-on to the active CICS
region are to remain signed-on following a persistent sessions restart or an XRF takeover.
RSTSIGNOFF={NOFORCE|FORCE}
It applies to the following events:
```
- A persistent sessions restart, where PSDINT= _value_ and PSTYPE=SNPS or MNPS are specified, and
    the restart follows a CICS abnormal or immediate shutdown.
- A persistent sessions restart, where PSDINT= _value_ and PSTYPE=MNPS are specified, and terminal
    sessions are recovered as a result of a z/OS Communications Server restart.
- An XRF takeover, where XRF=YES is specified.
**NOFORCE**
    Do not sign off users, unless FORCE is specified on either:
    - The RSTSIGNOFF parameter in the TYPETERM definition referenced by the user's terminal
       definition.
    - The XRFSOFF parameter in the CICS segment of the user's RACF profile.
    Thus for a user to remain signed on after a persistent sessions restart or an XRF takeover,
    NOFORCE must be specified as a system initialization parameter, on the TYPETERM definition, and
    in the CICS segment.
**FORCE**
    Sign off all users regardless of the options specified on:
    - The RSTSIGNOFF attribute in the TYPETERM definition referenced by the user's terminal
       definition.
    - The **XRFSOFF** parameter in the CICS segment of the user's RACF profile.
See The CICS segment in user profiles for information about user profile options in the CICS segment,
and see TYPETERM resources for information about the TYPETERM resource definition.

## RSTSIGNTIME..........................................................................................................................................

```
The RSTSIGNTIME parameter specifies the timeout delay interval for signon retention during a persistent
sessions restart or an XRF takeover.
RSTSIGNTIME={ 500 |decimal-value}
You can specify a 1-to-6 digit time in hours, minutes and seconds, up to the maximum time of 23
hours 59 minutes 59 seconds. If you specify less than six digits, CICS pads the value with leading
zeros. Thus a value of 500 is taken as five minutes exactly.
RSTSIGNTIME is counted from the time when CICS failed. Note that the time of failure cannot be
determined with complete accuracy.
If you specify NOFORCE on all the appropriate parameters to enable a user to remain signed on, but
the persistent sessions restart or XRF takeover takes longer than the specified on the RSTSIGNTIME
parameter, CICS ensures users do not remain signed on after the delay period expires.
500
Five minutes is the default value.
time
This is the time, in the range 0 through 23 hours 59 minutes 59 seconds, during which CICS
permits users to remain signed on during a persistent sessions restart or an XRF takeover. The
period is measured as follows:
```
- For a persistent sessions restart, the period is the time from the CICS failure and the time when
    the user starts working on the terminal. If the specified time expires before the user starts

**114**   CICS TS for z/OS: System Initialization Parameter Reference


```
working on the terminal, users signed on at the time CICS failed are not signed on again after
restart.
```
- For an XRF takeover, the period is the time from when the takeover is initiated to the time at
    which the alternate CICS has completed takeover and is ready to process user transactions. If
    the takeover takes longer than the specified period, all users signed on at the time the takeover
    was initiated are signed off.
A value of 0 means there is no timeout delay, and terminals are not signed on after a persistent
sessions restart or XRF takeover, which means that RSTSIGNTIME=0 has the same effect as
coding RSTSIGNOFF=FORCE.
When XRF is in use with non-XRF-capable terminals, take into account any AUTCONN delay period
when setting the value for RSTSIGNTIME. For example, you might need to increase the time
specified on RSTSIGNTIME to allow for the delay up to the start of the CXRE transaction imposed
by the AUTCONN parameter; otherwise, terminals could be signed off too early.

## RUWAPOOL..............................................................................................................................................

```
The RUWAPOOL parameter specifies the option for allocating a storage pool the first time a program
invoked by Language Environment runs in a task.
RUWAPOOL={NO|YES}
Valid values are as follows:
NO
CICS disables the option and provides no RUWA storage pool. Every EXEC CICS LINK to a
program that runs under Language Environment results in a GETMAIN for RUWA storage.
YES
CICS creates a pool of storage the first time a program invoked by Language Environment runs in
a task. This provides an available storage pool that reduces the need to GETMAIN and FREEMAIN
run-unit work areas (RUWAs) for every EXEC CICS LINK request.
Note: This applies only to application programs running with the Language Environment runtime
option ALL31(ON). RUWAPOOL=YES has no effect on application programs running with the
Language Environment runtime option ALL31(OFF).
```
## SDSASZE..................................................................................................................................................

```
The SDSASZE system initialization parameter specifies the size of the SDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
SDSASZE={0K|number}
Valid values are as follows:
0 (zero)
The size of the SDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the SDSA dynamic storage area is fixed. Specify number
as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes (256 KB).
If the value you specify is not a multiple of 256 KB, CICS rounds up the value to the next multiple.
You can specify number as a number of bytes, a whole number of kilobytes, or a whole number of
megabytes. Use the letter M to indicate that the value represents a whole number of megabytes
(for example, 4 M). Use the letter K to indicate that the value represents a whole number of
```
```
Chapter 1. System initialization parameter summary   115
```

```
kilobytes (for example, 4096 K), in which case the number is rounded up to the number of
megabytes.
Restriction: You can specify the SDSASZE parameter in PARM, SYSIN, or CONSOLE only.
```
## SDTMEMLIMIT.........................................................................................................................................

```
The SDTMEMLIMIT system initialization parameter specifies a limit to the amount of storage above the bar
that is available for shared data tables to use for control information (entry descriptors, backout elements,
and index nodes). The default is 4 GB. When you set this parameter, check your current setting for the
z/OS MEMLIMIT parameter.
Important: You can specify an amount of storage in the range 1 through 524288 MB (512 GB), but this
amount must not be greater than 40% of the z/OS MEMLIMIT value. MEMLIMIT limits the amount of
64-bit storage that the CICS address space can use. If you set SDTMEMLIMIT to a value greater than 40%
of the MEMLIMIT value, message DFHFC0418 is issued and CICS terminates.
For information about the MEMLIMIT value for CICS and instructions to check the MEMLIMIT value that
currently applies to the CICS region, see Estimating and checking MEMLIMIT. For information about the
z/OS MEMLIMIT parameter, see Limiting the use of private memory objects in the z/OS MVS Programming:
Extended Addressability Guide.
SDTMEMLIMIT={4G|nnnnnnM|nnnG}
Valid values are as follows:
4G
The default amount of storage above the bar that is available for shared data tables to use.
nnnnnnM
Specifies an amount of storage above the bar, in megabytes, that is available for shared data
tables to use. It can have a value in the range 1 through 524288 MB.
nnnG
Specifies an amount of storage above the bar, in gigabytes, that is available for shared data tables
to use. It can have a value in the range 1 through 512 GB.
```
## SDTRAN....................................................................................................................................................

```
The SDTRAN system initialization parameter specifies the name of the shutdown assist transaction to be
started at the beginning of normal and immediate shutdown.
SDTRAN={CESD| name_of_shutdown_tran |NO}
The shutdown assist transaction enables CICS to shut down in a controlled manner, within a
reasonable period of time. For example, you can use it to purge and backout long-running tasks,
while ensuring that as many tasks as possible commit or back out cleanly. For information about the
CICS-supplied program, DFHCESD, started by the default shutdown assist transaction, CESD, and how
to use it as the basis for your own transaction, see Shutdown assist program (DFHCESD).
Note:
```
1. The transaction runs under the user ID authority of the issuer of the shutdown command. For more
    information, see Security for the shutdown assist program.
2. If the program named by the shutdown assist transaction cannot be loaded, CICS waits indefinitely
    for all user tasks to complete. _This happens on an immediate, as well as on a normal, shutdown_.
**CESD**
Starts the CICS-supplied program DFHCESD.
**_name_of_shutdown_transaction_**
The 1- to 4-character name of your own shutdown assist transaction.
**NO**
Do not run a shutdown assist transaction. On a normal shutdown, CICS waits indefinitely for all
user tasks to complete.

**116**   CICS TS for z/OS: System Initialization Parameter Reference


## SEC...........................................................................................................................................................

```
The SEC system initialization parameter specifies what level of external security you want CICS to use.
SEC={YES|NO}
Valid values are as follows:
YES
You want to use full external security. CICS requires the appropriate level of authorization for
the access intent: a minimum of READ permission for read intent, and a minimum of UPDATE
permission for update intent.
Note: You must also ensure that the default user ID (CICSUSER or another user ID specified on
the DFLTUSER system initialization parameter) has been defined to RACF.
If command security checking is defined for CICS SP-type commands, then specifying SEC=YES
means that the appropriate level of authority is checked for; therefore:
```
- A check for READ authority is made for **INQUIRE** and **COLLECT** commands.
- A check for UPDATE authority is made for **SET** , **PERFORM** , and **DISCARD** commands.
**NO**
You do not want CICS to use RACF. All users have access to all resources, whether determined by
attempts to use them or by the **QUERY SECURITY** command. Users are not allowed to sign on or
off.
**Note:** With MRO bind-time security, even if you specify SEC=NO, the CICS region user ID is still
sent to the secondary CICS region, and bind-time checking is still carried out in the secondary
CICS region. For information about MRO bind-time security, see MRO connection (bind-time)
security.
Define whether to use RACF for resource level checking by using the **XDCT** , **XFCT** , **XHFS** , **XJCT** ,
**XPCT** , **XPPT** , **XPSB** , **XRES** , and **XTST** system initialization parameters. Define whether to use RACF
for transaction security checking by using the **XTRAN** system initialization parameter. Define whether
RACF session security can be used when establishing APPC sessions by using the **XAPPC** system
initialization parameter.
For programming information about the use of external security for CICS system commands, see
Security checking.
**Restriction:** You specify the **SEC** parameter in the SIT system initialization parameter, PARM option,
or SYSIN control statement.
**Note:** If you are using preset terminal security and you perform a warm start with SEC=NO and then
again with SEC=YES, you must reinstall the terminal definition to preserve the preset user ID that is
replaced by the default user ID when security is switched off. See Preset terminal security for details.

## SECPRFX..................................................................................................................................................

```
The SECPRFX system initialization parameter specifies whether CICS prefixes the resource names in any
authorization requests to RACF.
SECPRFX={NO|YES| prefix }
Valid values are as follows:
NO
CICS does not use prefixes on any resource names.
YES
CICS prefixes all resource names with the CICS region user ID. This is the user ID under which the
CICS job runs. It is one of the following:
```
- If CICS is a batch job, it is the user ID corresponding to the USER parameter of the CICS JOB
    statement.

```
Chapter 1. System initialization parameter summary   117
```

- If CICS is a started task, it is the user ID associated with the name of the started procedure in
    the RACF ICHRIN03 table.
- If CICS is a started job, it is the user ID specified in the user parameter of the STDATA segment
    of a STARTED general resource class profile.
For more information, see Specifying the CICS region user ID.
**_prefix_**
CICS prefixes all resource names with the string you specify. It can be any string of 1 to 8
uppercase alphanumeric characters except NO or YES, and it must start with an alphabetic
character.
The SECPRFX parameter is effective only if you specify YES for the SEC system initialization
parameter.
**Restriction:** You can specify the SECPRFX parameter in the SIT, PARM, or SYSIN only.

## SIT............................................................................................................................................................

```
The SIT system initialization parameter specifies the suffix, if any, of the system initialization table that
you want CICS to load at the start of initialization.
SIT= xx
If you omit this parameter, CICS loads the unsuffixed table, DFHSIT, which is generated with all
the default values. This default SIT (shown in The default system initialization table) is in the
CICSTS nn .CICS.SDFHAUTH library, where CICSTS nn is your version of CICS. As an example, for
CICS Transaction Server for z/OS, Version 6 Release 2, this is CICSTS62.CICS.SDFHAUTH.
The source of the default SIT, named DFHSIT$$, is in the CICSTS nn .CICS.SDFHSAMP library, where
CICSTS nn is your version of CICS. As an example, for CICS Transaction Server for z/OS, Version 6
Release 2, this is CICSTS62.CICS.SDFHSAMP.
Restriction: You can specify the system initialization parameter anywhere in PARM or SYSIN, or as the
first parameter entry at the CONSOLE.
```
## SKRxxxx...................................................................................................................................................

```
The SKRxxxx system initialization parameter specifies that a single-keystroke-retrieval operation is
required.
SKRxxxx='page-retrieval-command'
'xxxx' specifies a key on the 3270 keyboard which, during a page retrieval session, is to be used
to represent a page retrieval command. The valid keys you can specify as a system initialization
parameter or as an override are PA1 through PA3, and PF1 through PF24.  Therefore it is possible to
specify up to 27 keys in total.
The 'page-retrieval-command' value represents any valid page retrieval command, and must be
enclosed in apostrophes. It is concatenated to the character string coded in the PGRET parameter.
The combined length must not exceed 16 characters.
Note: If full function BMS is used, all PA keys and PF keys are interpreted for page retrieval
commands, even if some of these keys are not defined.
```
**118**   CICS TS for z/OS: System Initialization Parameter Reference


## SNPRESET................................................................................................................................................

```
The SNPRESET system initialization parameter specifies whether preset userid terminals share a single
access control environment element (ACEE) that is associated with the userid, or a unique ACEE for every
terminal.
SNPRESET={UNIQUE|SHARED}
UNIQUE
When signing on a preset userid terminal, the ACEE will be built with entry port information. Every
preset terminals will have a unique ACEE that is associated with the userid and terminal. This is
the default.
If you audit data that is based on the terminal of a preset userid, use SNPRESET=UNIQUE.
SHARED
When signing on a preset userid terminal, the ACEE will be built without entry port information. All
preset terminals with the same userid will use the same ACEE.
If you do not need information that is based on the terminal of a preset userid, you can save
storage by selecting SNPRESET=SHARED.
Note: Set SNPRESET=SHARED only when you have a large number of preset userid terminals and do
not have security definitions that rely on the netname of these terminals.
In the event of a security violation with SNPRESET=SHARED, the netname of the terminal will not
appear in the DFHXS1111 message.
```
## SNSCOPE..................................................................................................................................................

```
The SNSCOPE system initialization parameter specifies whether a userid can be signed on to CICS more
than once, within the scope of a single CICS region, a single z/OS image, and a sysplex.
SNSCOPE={NONE|CICS|MVSIMAGE|SYSPLEX}
The sign-on SCOPE is enforced with the zOS ENQ macro where there is a limit on the number of
outstanding zOS ENQs per address space. If this limit is exceeded, the zOS ENQ is rejected and CICS
is unable to detect if the user is already signed on. When this happens, the sign on request is rejected
with message DFHCE3587. You can use the ISGADMIN macro to set or reset the zOS ENQ limit. See
the z/OS MVS Programming: Authorized Assembler Services Reference (Volume 2).
NONE
Each user ID can be used to sign on for any number of sessions on any CICS region. This is the
compatibility option, providing the same sign-on scope as previous releases of CICS.
CICS
Each user ID can be signed on once only in the same CICS region. A sign on request is rejected if
the user ID is already signed on to the same CICS region. However, the user ID can be used to sign
on to another CICS region in the same, or another, zOS image.
MVSIMAGE
Each userid can be signed on once only, and to only one of the set of CICS regions in the same zOS
image that also specify SNSCOPE=MVSIMAGE. A sign-on request is rejected if the user is already
signed on to another CICS region in the same zOS image.
SYSPLEX
Each user ID can be signed on once only, and to only one of the set of CICS regions within an zOS
sysplex that also specify SNSCOPE=SYSPLEX. A sign on is rejected if the user is already signed on
to another CICS region in the same zOS sysplex.
The sign-on scope (if specified) applies to all user IDs signing on by an explicit sign on request (for
example, by an EXEC CICS SIGNON command or the CESN transaction). SNSCOPE is restricted to
users who sign on at local terminals, or who sign on after using the CRTE transaction to connect to
another system.
Sign-on scope as specified by SNSCOPE does not apply to:
```
```
Chapter 1. System initialization parameter summary   119
```

- Non-terminal users.
- The CICS default userid, specified by the **DFLTUSER** system initialization parameter.
- Preset user IDs, specified in the USERID option of the **DEFINE TERMINAL** command.
- User IDs for remote users, received in attach headers.
- User IDs for link security. For information about which userid is used for link security on a specific
    connection, see Security-related system initialization parameters.
- The user ID specified on the **PLTPIUSR** system initialization parameter.
- The CICS region user ID.
**Restriction:** You can specify the **SNSCOPE** parameter in the SIT, PARM, or SYSIN only.

## SOTUNING...............................................................................................................................................

```
The SOTUNING system initialization parameter specifies whether performance tuning for HTTP
connections will occur to protect CICS from unconstrained resource demand.
For more information about performance tuning for HTTP connections, see CICS HTTP support:
Performance and tuning.
SOTUNING={YES|520}
Valid values are as follows:
YES
As a region becomes overloaded, CICS will pause listening for new HTTP connection requests.
While new connection requests are not being accepted, those pending requests will queue outside
of CICS in the TCP/IP backlog queue. This backlog queue will increase when the region is over
capacity, allowing feedback to TCP/IP port sharing and Sysplex Distributor, promoting a balanced
sharing of workload with other regions that are sharing the same IP endpoint.
Because requests are no longer queuing in CICS, MXT will not be exceeded by a surge of HTTP
requests, but the number of times MXT is reached might greatly increase. As CICS processes
requests from the backlog queue, the number of active tasks will fluctuate, potentially reaching
MXT multiple times.It does not mean that MXT needs to be increased, but indicates that the
current value is correctly protecting CICS from unconstrained resource demand.
If the region continues to become overloaded, it will close existing persistent connections after
their next request completes and new connections will be marked as non-persistent until the
region is no longer under stress.
In addition, CICS will also periodically close persistent connections to allow more efficient sharing
of workload across regions that share IP endpoints.
520
The CICS TS V5.2 behavior is used, and performance tuning for HTTP connections does not take
place.
Note: If sharing IP endpoints, ensure that all regions have the same SOTUNING value or uneven loading
might occur.
```
## SPCTR.......................................................................................................................................................

```
The SPCTR system initialization parameter specifies the level of special tracing required for CICS as a
whole.
SPCTR={(1,2 )|(1[,2][,3])|ALL|OFF}
Specifies the level of special tracing for all CICS components used by a transaction, terminal, or both.
If you want to set different tracing levels for an individual component of CICS, use the SPCTRxx
system initialization parameter.
```
**120**   CICS TS for z/OS: System Initialization Parameter Reference


```
It is possible to select up to 4 levels of tracing using this parameter. However, most CICS components
only use levels 1, 2, and 3, and some do not have trace points at all these levels. The exception is the
SM component (storage manager domain), which also has level 4 tracing. Use the SPCTRxx system
initialization parameter to set special tracing levels above 3 for this component.
number
The level numbers for the level of special tracing you want for all CICS components.
ALL
Enables the special tracing facility for all available levels.
OFF
Disables the special tracing facility.
```
## SPCTRxx...................................................................................................................................................

```
The SPCTRxx system initialization parameter specifies the level of special tracing for a particular CICS
component used by a transaction, terminal, or both.
SPCTRxx={(1,2)|(1[,2][,3][,4][,5])|ALL|OFF}
You identify the component by coding a value for xx in the keyword. You code one SPCTRxx keyword
for each component that you want to define selectively. For a CICS component that is being specially
traced and that does not have its trace level set by SPCTRxx, the trace level is that set by SPCTR ,
which, in turn, defaults to (1,2). The CICS component codes that you can specify for xx on the
SPCTRxx keyword are shown in Table 4 on page 121.
number
The level numbers for the level of special tracing you want for the required CICS component. You
can use level numbers 1, 2, 3, 4 and 5, depending on the component.
Most CICS components only use levels 1, 2 and 3, and some do not have trace points at all these
levels. The exceptions are the SM and SJ component (storage manager domain) that have level 4
and level 5 tracing respectively. This level of tracing is intended for IBM Support.
ALL
You want all the available levels of special CICS tracing switched on for the specified component.
OFF
Switches off all levels of special CICS tracing for the CICS component indicated by xx.
For details of using trace, see Using CICS trace for problem determination.
Restriction: You can specify the SPCTRxx parameter in PARM, SYSIN, or CONSOLE only.
```
```
Table 4. CICS component code
```
```
Code Component name
```
```
AP Application domain
```
```
AS Asynchronous services
```
```
BA Business application manager
```
```
BF* Built-in function
```
```
BM* Basic mapping support
```
```
BR* 3270 bridge
```
```
CP* Common programming interface
```
```
DC* Dump compatibility layer
```
```
DD Directory manager domain
```
```
DH Document handling domain
```
```
Chapter 1. System initialization parameter summary   121
```

```
Table 4. CICS component code (continued)
```
```
Code Component name
```
```
DI* Data interchange
```
```
DM Domain manager domain
```
```
DP Debugging profiles domain
```
```
DS Dispatcher domain
```
```
DU Dump domain
```
```
EC* Event capture and emission
```
```
EI* Exec interface
```
```
EJ Enterprise Java domain
```
```
EM Event manager domain
```
```
EP Event processing domain
```
```
FC* File control
```
```
GC Global catalog domain
```
```
IC* Interval control
```
```
IE ECI over TCP/IP domain
```
```
IS* ISC or IRC
```
```
KC* Task control
```
```
KE Kernel
```
```
LC Local catalog domain
```
```
LD Loader domain
```
```
LG Log manager domain
```
```
LM Lock domain
```
```
ME Message domain
```
```
ML Markup language domain
```
```
MN Monitoring domain
```
```
MP Managed platform domain
```
```
NQ Enqueue domain
```
```
OT Object transaction domain
```
```
PA Parameter domain
```
```
PC* Program control
```
```
PG Program manager domain
```
```
PI Pipeline domain
```
```
PT Partner domain
```
```
RA Resource manager adapters
```
```
RI* Resource manager interface (RMI)
```
**122**   CICS TS for z/OS: System Initialization Parameter Reference


```
Table 4. CICS component code (continued)
```
```
Code Component name
```
```
RL Resource life-cycle domain
```
```
RM Recovery manager domain
```
```
RO* Resource overrides
```
```
RS Region status domain
```
```
RX RRS-coordinated EXCI domain
```
```
RZ Request streams domain
```
```
SC* Storage control
```
```
SH Scheduler services domain
```
```
SJ JVM and Node.js runtime domain
```
```
SM Storage manager domain
```
```
SO Sockets domain
```
```
ST Statistics domain
```
```
SZ* Front End Programming Interface
```
```
TC* Terminal control
```
```
TD* Transient data
```
```
TI Timer domain
```
```
TR Trace domain
```
```
TS Temporary storage domain
```
```
UE* User exit interface
```
```
US User domain
```
```
WB Web domain
```
```
WU® CICS Management Client Interface (CMCI) domain
```
```
W2 Web 2.0 domain
```
```
XM Transaction manager domain
```
```
XS Security manager domain
```
## SPOOL......................................................................................................................................................

```
The SPOOL system initialization parameter specifies whether the system spooling interface is required.
SPOOL={NO|YES}
Valid values are as follows:
NO
The system spooling interface is not required.
YES
The system spooling interface is required.
The CICS spool interface uses the z/OS exit IEFDOIXT, which is provided in the SYS1.LINKLIB library.
For further information about the z/OS exit IEFDOIXT, see z/OS MVS Installation Exits.
```
```
Chapter 1. System initialization parameter summary   123
```

## SRBSVC....................................................................................................................................................

```
The SRBSVC system initialization parameter specifies the number that you have assigned to the CICS type
6 SVC.
SRBSVC={ 215 |number}
The default number is 215.
For information on changing the SVC number, see Installing the CICS SVCs. A CICS type 6 SVC with
the specified (or default) number must have been link-edited with the system nucleus.
System initialization parameters to set up a CICS region summarizes the SIT parameters that you
must configure, or change from their default values, to set up a CICS region. The system initialization
parameters that you might consider whether to configure are also listed. For parameters that are not
listed in the following sections, it is unlikely that you need to change them from their defaults unless there
are specific requirements for your environment.
```
## SRT...........................................................................................................................................................

```
The SRT system initialization parameter specifies the system recovery table suffix. The system recovery
table (SRT) contains a list of codes for abends that CICS intercepts.
SRT={1$|YES|NO| xx }
If SRT=YES is coded, the default DFHSRT1$ table is used.
Restriction: SRT=YES can only be specified when assembling the SIT table; it cannot be specified as
an override parameter.
If SRT=NO is coded, the system recovery program (DFHSRP) does not attempt to recover from a
program check or from an operating system abend. However, CICS issues ESPIE macros to intercept
program checks to perform clean up operations before CICS terminates. Therefore, you must provide
a SRT if you require recovery from either program checks or abnormal terminations, or both. For
information about coding the macros for this table, see SRT - system recovery table.
```
## SRVERCP..................................................................................................................................................

```
The SRVERCP system initialization parameter specifies the default server code page to be used by the
DFHCNV data conversion table but only if the SRVERCP parameter in the DFHCNV macro is set to SYSDEF.
SRVERCP={ 037 | code page }
The code page is a field of up to 8 characters and can take the values supported by the SRVERCP
parameter in the DFHCNV macro. For the list of valid code pages, see CICS-supported conversions.
The default is 037.
You define the conversion table with DFHCNV resource definition macros. The output of the DFHCNV
macro assembly contains templates specifying resource conversion requirements and conversion tables
to enable the required conversions. User-generated conversion tables must be placed in the DFHCNV
macro source. For details, see Assembling and link-editing the conversion programs.
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The CLINTCP system initialization parameter
```
**124**   CICS TS for z/OS: System Initialization Parameter Reference


```
The CLINTCP parameter specifies the default client code page to be used by the DFHCNV data conversion
table, but only if the CLINTCP parameter in the DFHCNV macro is set to SYSDEF.
```
## SSLCACHE................................................................................................................................................

```
The SSL cache is used to store information about the SSL sessions between clients and CICS. It allows
CICS to perform abbreviated handshakes with clients that it has previously authenticated. Use the
SSLCACHE system initialization parameter to specify whether information about the SSL sessions are
to be cached locally or at sysplex level for reuse by the CICS region.
Sharing information about the SSL session across different CICS regions in a sysplex is particularly useful
when HTTP requests are being routed across a set of CICS regions by using TCP/IP connection workload
balancing techniques, such as TCP/IP port sharing or Sysplex Distributor. Consider using sysplex caching
if you have multiple CICS socket-owning regions that accept SSL connections at the same IP address. If
appropriate for your CICS systems, using sysplex caching can significantly reduce the number of full SSL
handshakes.
SSLCACHE={CICS|SYSPLEX}
CICS
The SSL environment for the CICS region includes a local cache of information about the SSL
sessions between CICS and clients. z/OS System SSL manages the SSL environment. This cache is
replaced by a new cache when the PERFORM SSL REBUILD command is issued.
SYSPLEX
A cache of SSL sessions is held at sysplex level for multiple CICS regions. This cache is not
affected when the PERFORM SSL REBUILD command is issued. You must activate the z/OS
System SSL started task GSKSRVR to have a sysplex cache. For details of the SSL started task
GSKSRVR and its configuration, see The SSL started task GSKSRVR.
To use the sysplex session cache, each system in the sysplex must be using the same external
security manager, and a user ID on one system in the sysplex must represent the same user on all
other systems in the sysplex.
To use sysplex caching for TLS 1.3, you must use z/OS 2.5 with APAR OA63252 (HA63252,
IA63252, and JA63252) or a later release of z/OS.
```
```
Restriction:
6.1
Sysplex caching by using the SYSPLEX option is not supported for TLS 1.3.
For difference in mechanisms for session caching between TLS 1.2 and TLS 1.3, see Sysplex session
cache support (TLS 1.2) in z/OS documentation and Sysplex session ticket cache support (TLS 1.3)
in z/OS documentation. For performance comparison between TLS 1.2 and TLS 1.3, see 6.2: TLS
comparison.
```
## SSLDELAY.................................................................................................................................................

```
The SSLDELAY system initialization parameter specifies the length of time in seconds for which CICS
retains session IDs for secure socket connections.
SSLDELAY={ 600 | number }
Session IDs are tokens that represent a secure connection between a client and an SSL server.
While the session ID is retained by CICS within the SSLDELAY period, CICS can continue to
communicate with the client without the significant overhead of an SSL handshake. The value is a
number of seconds in the range 0 through 86400.
```
## START.......................................................................................................................................................

```
The START system initialization parameter specifies the type of start for the system initialization program.
START=({AUTO|INITIAL|COLD|STANDBY}[,ALL])
The value specified for START, or the default of AUTO, becomes the default value for each resource.
```
```
Chapter 1. System initialization parameter summary   125
```

#### AUTO

```
CICS performs a warm, emergency, cold or initial start, according to the status of two control
records on the global catalog:
```
- The recovery manager (RM) control record written by the previous execution of CICS
- The RM autostart override record written by a run of the recovery manager utility program,
    DFHRMUTL
**Note:** If the global catalog does _not_ contain the RM control record:
- If it contains an RM autostart override record with option AUTOINIT, CICS performs an initial
    start.
- If it does not contain an RM autostart override record with option AUTOINIT, CICS does not
    start.
If you code START=AUTO, you must do one of the following:
- Provide the global catalog and system log from the previous execution of CICS. For an
    emergency restart to be successful, you must also have coded an activity keypoint value (see
    the “AKPFREQ” on page 19 parameter) on the previous execution of CICS.
- Provide a global catalog against which you have run the DFHRMUTL utility program, specifying
    SET_AUTO_START=AUTOINIT.
You may choose to leave the START parameter set to AUTO for all types of startup other than XRF
standby, and use the DFHRMUTL program to reset the startup mode to COLD or INITIAL when
necessary, using SET_AUTO_START=AUTOCOLD or SET_AUTO_START=AUTOINIT, respectively. For
information about the DFHRMUTL utility program, see Recovery manager utility (DFHRMUTL).
**INITIAL**
The status of CICS resource definitions saved in the global catalog at the previous shutdown is
ignored, and all resource definitions are reinstalled, either from the CSD or CICS control tables.
You should rarely need to specify START=INITIAL; if you want to reinstall definitions of local
resources from the CSD, use START=COLD instead.
Examples of times when an initial start is necessary are:
- When bringing up a new CICS system for the first time.
- After a serious software failure, when the system log has been corrupted.
- If the global catalog is cleared or initialized.
- When you want to run CICS with a dummy system log. (If the system log is defined as a dummy,
it is ignored.)
**COLD**
The status of CICS resource definitions saved in the global catalog at the previous shutdown is
ignored, and all resource definitions (except those for the system log) are reinstalled, either from
the CSD or CICS control tables.
Resynchronization information in the global catalog relating to remote systems or to RMI-
connected resource managers is preserved. The CICS system log is scanned during startup,
and information regarding unit of work obligations to remote systems, or to non-CICS resource
managers (such as Db2) connected through the RMI, is preserved. (That is, any decisions about
the outcome of local UOWs, needed to allow remote systems or RMI resource managers to
resynchronize their resources, are preserved.)
Note that, on a cold start, the following are _not_ preserved:
- Updates to _local_ resources that were not fully committed or backed out during the previous
execution, _even if the updates were part of a distributed unit of work_.
- Resynchronization information for remote systems connected by LU6.1 links, or for earlier
releases of CICS systems connected by MRO.

**126**   CICS TS for z/OS: System Initialization Parameter Reference


- Any program LIBRARY definitions that had been dynamically defined. Only the static DFHRPL
    concatenation will remain, together with any LIBRARY definitions in the grouplist specified at
    startup or installed via BAS at startup.
If you want to reinstall resource definitions from the CSD, use START=COLD rather than
START=INITIAL.
**STANDBY**
Coding START=STANDBY, but only when you have also specified XRF=YES, defines this CICS as
the alternate CICS region in an XRF pair. In other words, you **must** specify START=STANDBY for
the system that starts off as the alternate. (To start an active CICS region, specify AUTO or COLD,
as you would without XRF.)
**(option,ALL)**
The ALL option is a special option you can use on the START parameter when you supply it as
a system initialization parameter at CICS startup; you cannot code it in the SIT. If you specify
START=(AUTO,ALL), CICS initializes all resources according to the type of startup that it selects
(warm, emergency, initial, or cold). The ALL option overrides any individual settings in other
system initialization parameters.
However, if you do not use the ALL option, you can individually cold start those resources that
have a COLD operand. For details of resources that have a COLD option, see Defining CICS
resource table and module keywords.
**Restriction:** You can specify START=(option,ALL) in PARM, SYSIN, or CONSOLE only.
For more information about the types of CICS startup, see Controlling start and restart.

## STARTER..................................................................................................................................................

```
The STARTER system initialization parameter is used only by the DFHSIT macro. It specifies whether the
generation of starter system modules with $ and # suffixes is permitted and whether various MNOTES are
suppressed.
STARTER={NO|YES}
Run the DFHSIT macro with STARTER=YES if you need to work on the sample modules, such as
DFHSIT6$. A SIT can have a suffix of $ or # (for example, the CICS sample SIT is DFHSITx$) but you
can assemble such a SIT only when DFHSIT is run with STARTER=YES.
Restriction: You can specify the STARTER parameter only in the DFHSIT macro.
```
## STATEOD..................................................................................................................................................

```
The STATEOD system initialization parameter specifies the end-of-day time in the format hhmmss.
STATEOD={ 0 |hhmmss}
The default is 0, which is midnight.
End-of-day time is expressed in local time and must be in the range 00:00:00-23:59:59. That is, the
hh value cannot exceed 23, and the mm and ss values can be specified in the range 00 to 59. If you
leave out leading zeros, the DFHSIT macro inserts them (for example, 100 becomes 000100—that is,
1 minute 00 seconds past midnight).
This parameter is the equivalent of the ENDOFDAY option on the CEMT and EXEC CICS SET
STATISTICS command, which you can use to modify the value set by STATEOD.
```
## STATINT...................................................................................................................................................

```
The STATINT system initialization parameter specifies the recording interval for system statistics in the
format hhmmss.
STATINT={ 010000 | hhmmss }
The default is 1 hour.
```
```
Chapter 1. System initialization parameter summary   127
```

```
The interval must be at least one minute and cannot be more than 24 hours. The minutes and seconds
part of the value can be specified in the range 00 to 59. If you leave out leading zeros, the DFHSIT
macro inserts them. For example, 3000 becomes 003000 (that is, an interval of 30 minutes).
This parameter is the equivalent of the INTERVAL option on the CEMT and EXEC CICS SET
STATISTICS command, which you can use to modify the value set by STATINT.
```
## STATRCD..................................................................................................................................................

```
The STATRCD system initialization parameter specifies the interval statistics recording status at CICS
initialization.
STATRCD={OFF|ON}
This status is recorded in the CICS global catalog for use during warm and emergency restarts.
Statistics collected are written to the SMF data set.
OFF
Interval statistics are not collected (no action is taken at the end of an interval).
End-of-day statistics are collected at the logical end of day and on shutdown. Unsolicited statistics
are written to SMF when resources are discarded or closed.
ON
Interval statistics are collected.
On a cold start of a CICS region, interval statistics are recorded by default at hourly intervals. All
intervals are timed using the end-of-day time as a base starting time (not CICS startup time). The
default end-of-day time is midnight, so the default settings result in collections at 00.00, 01.00,
02.00, 03.00, and so on, regardless of the time that you start CICS.
On a warm or emergency restart, the statistics recording status is restored from the CICS global
catalog.
You can change the statistics recording status at any time in the following ways:
```
- During a warm or emergency restart by coding the **STATRCD** system initialization parameter.
- While CICS is running by using the CEMT or EXEC CICS SET STATISTICS command.
Whatever the value of the **STATRCD** system initialization parameter, you can ask for requested
statistics and requested reset statistics to be collected. You can get statistics "on demand" for all,
or for specified, resource types by using CEMT PERFORM STATISTICS or the **PERFORM STATISTICS**
command. See CEMT PERFORM STATISTICS and PERFORM STATISTICS.
The period covered for statistics requested in this way is from the last reset time up to the time that
you issue the PERFORM STATISTICS command. The last reset time is one of the following:
- The beginning of the current interval.
- The logical end-of-day collection time.
- The time that you last issued a SET or PERFORM STATISTICS command specifying the RESETNOW
    option.
For information about the statistics utility program DFHSTUP, see Statistics utility program
(DFHSTUP).

## STGPROT..................................................................................................................................................

```
The STGPROT system initialization parameter specifies whether you want storage protection to operate in
the CICS region.
STGPROT={NO|YES}
The permitted values are YES (the default), or NO.
```
**128**   CICS TS for z/OS: System Initialization Parameter Reference


#### YES

```
If you specify YES, or allow this system initialization parameter to default, CICS operates with
storage protection, and observes the storage keys and execution keys that you specify in various
system and resource definitions.
NO
If you specify NO, CICS does not operate any storage protection.
See CICS dynamic storage areas (DSAs) for information about which DSAs are affected by the use of
STGPROT system initialization parameter. When CICS operates with storage protection, the storage for
these DSAs is allocated from user-key storage. When CICS operates without storage protection, the
storage for these DSAs is allocated from CICS-key storage.
```
## STGRCVY..................................................................................................................................................

```
The STGRCVY system initialization parameter specifies whether CICS should try to recover from a storage
violation.
STGRCVY={NO|YES}
Valid values are as follows:
NO
CICS does not try to repair any storage violation that it detects.
YES
CICS tries to repair any storage violation that it detects.
In both cases, CICS continues unless you have specified in the dump table that CICS should
terminate.
In normal operation, CICS sets up several task-lifetime storage subpools for each task. Each element
in the subpool starts and ends with a check zone that includes the subpool name. At each FREEMAIN
and at end of the task, CICS checks the check zones and abends the task if either has been
overwritten.
Terminal input-output areas (TIOAs) have similar check zones, which are set up with identical values.
At each FREEMAIN of a TIOA, CICS checks the check zones and abends the task if they are not
identical.
If you specify STGRCVY(YES) , CICS repairs the corrupted SAAs or check zones and the task
continues running. The overwriting of check zones is treated differently; CICS resets the check zones
to their initial values and the task continues running.
If you specify STGRCVY(NO) , CICS abends the task if it is still running. The storage is not reusable and
is not returned to the DSA for the remainder of the CICS cycle. If an error is detected when the task
ends, no abend is issued. Any syncpoint that has taken place could save data that is corrupted.
```
## STNTR......................................................................................................................................................

```
The STNTR system initialization parameter specifies the level of standard tracing required for CICS as a
whole.
STNTR={ 1 |(1[,2][,3])|ALL|OFF}
For standard system trace, use STNTR to specify a global trace level for all CICS components.
Most CICS components only use trace levels 1, 2, and 3, and some do not have trace points at all
these levels. The exceptions are the SM (storage manager domain) and SJ (JVM and Node.js runtime
domain) components. SM has trace levels 1 through 4, and SJ has trace levels 1 through 5. SM levels
3 and 4 tracing and SJ levels 4 and 5 tracing are intended for use by IBM Support.
If you need to set standard tracing levels above 3 for a component, use the STNTRxx system
initialization parameter, rather than the STNTR system initialization parameter.
```
```
Chapter 1. System initialization parameter summary   129
```

```
CAUTION: Using trace levels 3, 4 or ALL for standard tracing of the managed platform domain
(MP), the storage manager domain (SM), or the temporary storage domain (TS) degrades
the performance of your CICS region. These trace options are intended for use only by IBM
Support. For details about the effects of trace levels 3, 4 and 5, and the impact that these
trace options have on system performance, see Special considerations for AP, MP, SJ, and SM
components.
1
The default, 1, specifies standard level 1 tracing for all CICS components.
number
Code the level numbers for the level of standard tracing you want for all CICS components. The
options are as follows:
```
- STNTR=1
- STNTR=(1,2)
- STNTR=(1,2,3)
**ALL
Use with caution.** Enables standard tracing for all levels. There are up to 32 trace levels in CICS.
**OFF**
Disables standard tracing.
For information about the differences between special and standard CICS tracing, see How it works:
CICS system trace.

## STNTRxx...................................................................................................................................................

```
The STNTRxx system initialization parameter specifies the level of standard tracing you require for a
particular CICS component.
Restriction: You can specify the STNTRxx parameter in PARM, SYSIN, or CONSOLE only.
STNTRxx={ 1 |(1[,2][,3][,4][,5])|ALL|OFF}
You identify the component by coding a value for xx in the keyword. You code one STNTRxx keyword
for each component you want to define selectively. For a CICS component that does not have its trace
level set by STNTRxx, its trace level is determined by “STNTR” on page 129, which defaults to 1.
The CICS component codes that you can specify for xx on this STNTRxx keyword are shown in Table 5
on page 131.
number
Specify a number for the level of standard tracing you want for a CICS component that is identified
by component code xx. Level numbers 1, 2, 3, 4 and 5 can be used, depending on the component.
Most CICS components only use trace levels 1, 2, and 3, and some do not have trace points at
all these levels. The exceptions are the SM (storage manager domain) and SJ (JVM and Node.js
runtime domain) components. SM has trace levels 1 through 4, and SJ has trace levels 1 through
```
5. SM levels 3 and 4 tracing and SJ levels 4 and 5 tracing are intended for use by IBM Support.
**ALL
Use with caution.** You want all the available levels of standard tracing switched on for the
specified component.
**OFF**
Switches off all levels of standard CICS tracing for the CICS component indicated by xx.
**CAUTION:** Using trace levels 3, 4 or ALL for standard tracing of the managed platform domain
(MP), the storage manager domain (SM), or the temporary storage domain (TS) degrades the
performance of your CICS region. These trace options are intended for use only by IBM Support.
For details about the effects of trace levels 3, 4 and 5, and the impact that these trace options
have on system performance, see Special considerations for AP, MP, SJ, and SM components.

**130**   CICS TS for z/OS: System Initialization Parameter Reference


```
Table 5. CICS component code
```
**Code Component name**

AP Application domain

AS Asynchronous services

BA Business application manager

BF* Built-in function

BM* Basic mapping support

```
BR* 3270 bridge
```
```
CP* Common programming interface
```
```
DC* Dump compatibility layer
```
```
DD Directory manager domain
```
```
DH Document handling domain
```
```
DI* Data interchange
```
```
DM Domain manager domain
```
```
DP Debugging profiles domain
```
```
DS Dispatcher domain
```
```
DU Dump domain
```
```
EC* Event capture and emission
```
```
EI* Exec interface
```
```
EJ Enterprise Java domain
```
```
EM Event manager domain
```
```
EP Event processing domain
```
```
FC* File control
```
```
GC Global catalog domain
```
```
IC* Interval control
```
```
IE ECI over TCP/IP domain
```
```
IS* ISC or IRC
```
```
KC* Task control
```
```
KE Kernel
```
```
LC Local catalog domain
```
```
LD Loader domain
```
```
LG Log manager domain
```
```
LM Lock domain
```
```
ME Message domain
```
```
ML Markup language domain
```
```
MN Monitoring domain
```
```
Chapter 1. System initialization parameter summary   131
```

```
Table 5. CICS component code (continued)
```
```
Code Component name
```
```
MP Managed platform domain
```
```
NQ Enqueue domain
```
```
OT Object transaction domain
```
```
PA Parameter domain
```
```
PC* Program control
```
```
PG Program manager domain
```
```
PI Pipeline domain
```
```
PT Partner domain
```
```
RA Resource manager adapters
```
```
RI* Resource manager interface (RMI)
```
```
RL Resource life-cycle domain
```
```
RM Recovery manager domain
```
```
RO* Resource overrides
```
```
RS Region status domain
```
```
RX RRS-coordinated EXCI domain
```
```
RZ Request streams domain
```
```
SC* Storage control
```
```
SH Scheduler services domain
```
```
SJ JVM and Node.js runtime domain
```
```
SM Storage manager domain
```
```
SO Sockets domain
```
```
ST Statistics domain
```
```
SZ* Front End Programming Interface
```
```
TC* Terminal control
```
```
TD* Transient data
```
```
TI Timer domain
```
```
TR Trace domain
```
```
TS Temporary storage domain
```
```
UE* User exit interface
```
```
US User domain
```
```
WB Web domain
```
```
WU CICS Management Client Interface (CMCI) domain
```
```
W2 Web 2.0 domain
```
```
XM Transaction manager domain
```
**132**   CICS TS for z/OS: System Initialization Parameter Reference


```
Table 5. CICS component code (continued)
```
```
Code Component name
```
```
XS Security manager domain
```
```
Related reference
“System initialization parameter summary” on page 1
You can define system initialization (SIT) parameters to CICS in a DFHSIT macro, in a PARM parameter on
the EXEC PGM=DFHSIP statement, in the SYSIN data set of the CICS startup job stream, or through the
system console. This table lists all the SIT parameters and shows where each parameter can be defined.
Default values and descriptions are also included.
The STNTR system initialization parameter
The STNTR system initialization parameter specifies the level of standard tracing required for CICS as a
whole.
```
## SUBTSKS..................................................................................................................................................

```
The SUBTSKS system initialization parameter specifies the number of task control blocks (TCBs) you want
CICS to use for running tasks in concurrent mode.
SUBTSKS={ 0 |1}
Specifies whether there is to be a concurrent mode TCB so that CICS can perform management
functions as system subtasks.
0
If you specify 0 (the default), CICS runs under the following two TCBs:
The quasi-reentrant mode TCB
CICS runs all user applications under this TCB.
The resource-owning mode TCB
CICS runs tasks that open and close files under this TCB.
1
If you specify 1, CICS runs under the two TCBs listed previously, and uses an additional TCB, a
concurrent mode TCB, to perform system subtasking.
```
## SUFFIX.....................................................................................................................................................

```
The SUFFIX system initialization parameter specifies the last two characters of the name of this system
initialization table.
SUFFIX= xx
The first 6 characters of the name of the SIT are fixed as DFHSIT. You can specify the last two
characters of the name, using the SUFFIX parameter. Because the SIT does not have a TYPE=INITIAL
macro statement like other CICS resource control tables, you specify its SUFFIX on the TYPE=CSECT
macro statement.
The suffix allows you to have more than one version of the SIT. Any one or two characters (other
than NO and DY) are valid. You select the version of the table to be loaded into the system during
system initialization by coding SIT=xx in the PARM parameter or the SYSIN data set. (You can, in some
circumstances, specify the SIT using the system console, but this is not recommended.)
Restriction: You can specify the SUFFIX parameter in the SIT only.
```
```
Chapter 1. System initialization parameter summary   133
```

## SYDUMAX.................................................................................................................................................

```
The SYDUMAX system initialization parameter specifies the limit on the number of system dumps that can
be taken per dump table entry.
SYDUMAX={ 999 |number}
If this number is exceeded, subsequent system dumps for that particular entry will be suppressed.
The SYDUMAX parameter applies for new or added system dump codes. It does not override the limit
on the number of system dumps for existing dump table entries.
number
A number in the range 0 through 999. The default, 999, enables an unlimited number of dumps to
be taken.
```
## SYSIDNT...................................................................................................................................................

```
The SYSIDNT system initialization parameter specifies a 1- to 4-character name that is known only to
your CICS region.
SYSIDNT={CICS|name}
If your CICS region also communicates with other CICS regions, the name you choose for this
parameter to identify your local CICS region must not be the same name as an installed CONNECTION
resource definition for a remote region.
The value for SYSIDNT, whether specified in the SIT or as an override, can only be updated on a cold
start. After a warm start or emergency restart, the value of SYSIDNT is that specified in the last cold
start.
For information about the SYSIDNT of a local CICS region, see The local CICS region name.
```
## SYSTR.......................................................................................................................................................

```
The SYSTR system initialization parameter specifies the setting of the main system trace flag.
SYSTR={ON|OFF}
Valid values are as follows:
ON
The main trace flag is set, causing CICS to write trace entries of system activity for the individual
CICS components. Trace entries are captured and written only for those components for which the
trace level is 1 or greater, as specified on the STNTR or STNTRxx system initialization parameters.
Entries are written only to those trace destinations that are active.
OFF
The main trace flag is unset, and no standard trace entries are captured, overriding any trace
levels specified by the STNTR or STNTRxx system initialization parameters.
Note: Setting the main trace flag OFF affects only standard tracing and has no effect on
special tracing, which is controlled separately by SPCTR or SPCTRxx trace levels and the CETR
transaction.
See Using CICS trace for problem determination for more information about controlling CICS trace.
```
## TAKEOVR..................................................................................................................................................

```
The TAKEOVR system initialization parameter specifies the action to be taken by the alternate CICS
region, following the apparent loss of the surveillance signal in the active CICS region.
TAKEOVR={MANUAL|AUTO|COMMAND} (alternate)
Use this parameter in the SIT for an alternate CICS region. This parameter also specifies the level of
operator involvement.
```
**134**   CICS TS for z/OS: System Initialization Parameter Reference


```
If both active and alternate CICS regions are running under different MVS images in the same sysplex,
and an MVS failure occurs in the MVS image of the active CICS region, the TAKEOVR option is
overridden.
```
- If the MVS images are running in a PR/SM environment, CICS XRF takeover to an alternate CICS
    region on a separate MVS image completes without the need for any operator intervention.
- If the MVS images are not running in a PR/SM environment, the CICS takeover is still initiated
    automatically, but needs operator intervention to complete, because XCF outputs a WTOR
    (IXC402D). Sysplex partitioning does not complete until the operator replies to this message, and
    CICS waits for sysplex partitioning to complete before completing the XRF takeover.
**MANUAL**
    The operator is asked to approve a takeover if the alternate CICS region cannot detect the
    surveillance signal of the active CICS region.
    The alternate CICS region does not ask the operator for approval if the active CICS region signs off
    abnormally, or if there is an operator or program command for takeover. In these cases, there is
    no doubt that the alternate CICS region should take over, and manual involvement by the operator
    would be an unnecessary overhead in the takeover process.
    You could use this option, for instance, to ensure manual takeover of a main or coordinator region
    in MRO.
**AUTO**
    No operator approval, or intervention, is needed for a takeover.
**COMMAND**
    Takeover occurs only when a CEBT PERFORM TAKEOVER command is received by the alternate
    CICS region. It ensures, for instance, that a dependent alternate CICS region, in MRO, is activated
    only if it receives the command from the operator, or from a main or coordinator region.

## TBEXITS...................................................................................................................................................

```
The TBEXITS system initialization parameter specifies the names of your backout exit programs for use
during emergency restart backout processing.
TBEXITS=([name1][,name2][,name3] [,name4][,name5][,name6])
The order in which you code the names is significant. If you do not want to use all the exits, code
commas in place of the names you omit. For example:
```
```
TBEXITS=(,,EXITF,EXITV)
```
```
The program names for name1 through name6 apply to global user exit points as follows:
```
- _name1_ and _name2_ are the names of programs to be invoked at the XRCINIT and XRCINPT global
    user exit points (but note that XRCINIT and XRCINPT are invoked only for user log records).
- _name3_ is the name of the program to be invoked at the file control backout failure global user exit
    point, XFCBFAIL.
- _name4_ is the name of the program to be invoked at the file control logical delete global user exit
    point, XFCLDEL.
- _name5_ is the name of the program to be invoked at the file control backout override global user exit
    point, XFCBOVER.
- _name6_ is the name of the program to be invoked at the file control backout global user exit point,
    XFCBOUT.
This exit is invoked (if required) during backout of a unit of work, regardless of whether the backout is
taking place at emergency restart, or at any other time.
The XFCBFAIL, XFCLDEL, and XFCBOVER global user exit programs are enabled on all types of CICS
start if they are named on the TBEXITS system initialization parameter.
If no backout exit programs are required, you can do one of the following:

```
Chapter 1. System initialization parameter summary   135
```

- Omit the **TBEXITS** system initialization parameter altogether.
- Code the parameter as TBEXITS=(,,,,,).

## TCP...........................................................................................................................................................

```
The TCP system initialization parameter specifies whether the pregenerated non-z/OS Communications
Server terminal control program, DFHTCP, is to be included.
DFHTCP manages all non-z/OS Communications Server terminals, which involves:
```
- Ensuring that I/O operations are started when possible on the lines.
- Analyzing completion information.
- Attaching transactions when data is received from a terminal and no task is attached to that terminal.
- Servicing terminal control requests from user transactions.
**TCP={YES|NO}**
    You must code TCP=YES if you intend to use card reader/line printer (sequential) devices.

## TCPIP.......................................................................................................................................................

```
The TCPIP system initialization parameter specifies whether CICS TCP/IP services are to be activated at
CICS startup.
TCPIP={YES|NO}
YES
The IPIC, HTTP, and ECI over TCP/IP services can process work. This is the default value.
NO
The IPIC, HTTP, and ECI over TCP/IP services cannot be enabled.
For IPIC, you must specify TCPIP=YES and ISC=YES.
Note: The TCPIP system initialization parameter affects only CICS internal TCP/IP Services defined by
TCPIPSERVICE resource definitions. It has nothing to do with the TCP/IP socket interface for CICS feature
of z/OS Communications Server.
```
## TCSACTN..................................................................................................................................................

```
The TCSACTN system initialization parameter specifies the required action that CICS terminal control
should take if the terminal control shutdown wait threshold expires.
TCSACTN={NONE|UNBIND|FORCE}
For details of the wait threshold, see the TCSWAIT system initialization parameter. TCSACTN only
takes effect when TCSWAIT is coded with a value in the range 1 through 99. This is a global default
action. On a terminal-by-terminal basis, you can code a DFHZNEP routine to override this action.
NONE
No action is taken. This can be overridden by DFHZNEP.
```
- To report hung terminals and not attempt to force-close them specify the TCSWAIT=mm (with
    an appropriate time interval) and TCSACTN=NONE system initialization parameters.
- To attempt to force-close some hung terminals, and only report others, specify the
    TCSWAIT=mm (with an appropriate time interval) and TCSACTN=NONE system initialization
    parameters, and code a DFHZNEP routine that selects the required terminals and sets TWAOCN
    on for them.
**UNBIND**
CICS terminal control attempts to close the session by issuing a z/OS Communications Server
VTAM® CLSDST and sending an SNA UNBIND command to the hung terminal. This can be
overridden by DFHZNEP.

**136**   CICS TS for z/OS: System Initialization Parameter Reference


- To attempt to force-close all hung terminals specify the TCSWAIT=mm (with an appropriate time
    interval) and TCSACTN=UNBIND system initialization parameters.
**FORCE**
CICS terminal control attempts to forceclose the CICS z/OS Communications Server ACB if there
are any hung terminals or parallel connection sessions. All CICS z/OS Communications Server
terminals and sessions are released and CICS normal shutdown continues. This parameter will
only take effect if all LU Type 6.2 parallel connections, if any, have successfully completed CNOS
close processing.
- To attempt to force-close the CICS z/OS Communications Server ACB if there are any hung
terminals, specify the TCSWAIT=mm (with an appropriate time interval) and TCSACTN=FORCE
system initialization parameters.

## TCSWAIT..................................................................................................................................................

```
The TCSWAIT system initialization parameter specifies the required CICS terminal control shutdown wait
threshold.
TCSWAIT={ 4 |number|NO|NONE|0}
The wait threshold is the time, during shutdown, that CICS terminal control allows to pass before
it considers terminal shutdown to be hung. If all z/OS Communications Server sessions shutdown
and close before the threshold expires then the CICS shutdown process moves on to its next
stage, and the terminal control wait threshold then no longer applies. If, however, some of the z/OS
Communications Server sessions do not complete shutdown and close, then CICS takes special action
with these sessions. For details of this special action see the description of the TCSACTN system
initialization parameter. The wait threshold only applies to z/OS Communications Server sessions; that
is, z/OS Communications Server terminals and z/OS Communications Server intersystem connections.
The wait time is specified as a number of minutes, in the range 1 through 99. As a special case,
TCSWAIT=NO may be specified to indicate that terminal control shutdown is never to be considered
hung, no matter how long the shutdown and close process takes. TCSWAIT=NONE and TCSWAIT=0
are alternative synonyms for TCSWAIT=NO, and all three have the same effect (internally they are
held as the one value 0 (zero)).
The value that you specify on the TCSWAIT system initialization parameter should be large enough
so that under normal circumstances all z/OS Communications Server terminals and connections
shutdown in an orderly fashion. To help choose this value, consider using a value slightly larger than
the elapsed time between the following two CICS terminal control shutdown messages:
DFHZC2305 Termination of VTAM sessions beginning
DFHZC2316 VTAM ACB is closed
Note: VTAM is now z/OS Communications Server.
```
## TCT...........................................................................................................................................................

```
The TCT system initialization parameter specifies which terminal control table, if any, is to be loaded.
A CICS system can communicate with terminals, sequential devices, logical units, and other systems. The
terminal control table (TCT) defines each of the devices in the configuration. Each TCT entry defines the
optional and variable features of the device to CICS, and specifies the optional and variable features of
CICS to be used. For guidance about coding the macros for this table, see Terminal control table (TCT).
TCT={NO|xx|YES}
If you reassemble the TCT after starting CICS, any changes are applied when you next start CICS,
even if it is a warm or emergency startup.
If you have z/OS Communications Server-connected terminals only, you can specify TCT=NO. If you
do this, a dummy TCT called DFHTCTDY is loaded during system initialization. For more information
about DFHTCTDY, see The dummy TCT, DFHTCTDY. If you code TCT=NO, you must specify a CSD
group list in the GRPLIST parameter.
```
```
Chapter 1. System initialization parameter summary   137
```

### TCTUAKEY................................................................................................................................................

```
The TCTUAKEY system initialization parameter specifies the storage key for the terminal control table user
areas (TCTUAs) if you are operating CICS with storage protection (STGPROT=YES).
TCTUAKEY={USER|CICS}
The permitted values are USER (the default), or CICS:
USER
CICS obtains the amount of storage for TCTUAs in user key. This allows a user program executing
in any key to modify the TCTUA.
CICS
CICS obtains the amount of storage in CICS-key. This means that only programs executing in CICS
key can modify the TCTUA, and user-key programs have read-only access.
Only specify CICS key for TCTUAs when you are sure that this is justified. If you specify CICS-key
storage for TCTUAs, no user-key applications can write to any TCT user areas.
If CICS is running without storage protection, the TCTUAKEY parameter only designates which DSA
(User or CICS) the storage comes from. The TCTUAs are accessed in CICS-key whether they are in the
UDSA or CDSA.
```
### TCTUALOC................................................................................................................................................

```
The TCTUALOC system initialization parameter specifies where terminal user areas (TCTUAs) are to be
stored.
TCTUALOC={BELOW|ANY}
Valid values are as follows:
BELOW
The TCTUAs are stored in 24-bit storage (below the 16 MB line). If you require the terminal user
areas to be in 24-bit storage, because you have application programs that are not capable of
31-bit addressing, specify this setting.
ANY
The TCTUAs are stored anywhere in virtual storage. CICS stores TCTUAs in 31-bit storage (above
the 16 MB line) if possible. This setting is the default.
For more information about TCTUAs, see The TCTUA.
For details about defining terminals using RDO, see Model TERMINAL definitions in group DFHTERM.
```
### TD.............................................................................................................................................................

```
The TD system initialization parameter specifies the number of VSAM buffers and strings to be used for
intrapartition transient data (TD).
TD=({ 3 | decimal_value_1 }[,{ 3 | decimal_value_2 }])
Valid values are as follows:
decimal_value_1
The number of buffers to be allocated for the use of intrapartition transient data. The value must
be in the range 1 through 32 767. The default value is 3.
CICS obtains, above the 16 MB line, storage for the TD buffers in units of the page size (4 KB).
Because CICS optimizes the use of the storage obtained, TD may allocate more buffers than you
specify, depending on the control interval (CI) size you have defined for the intrapartition data set.
For example, if the CI size is 1536, and you specify 3 buffers (the default number), CICS allocates
5 buffers. This is because 2 pages (8192 bytes) are required to obtain sufficient storage for three
1536-byte buffers, a total of only 4608 bytes, which would leave 3584 bytes of spare storage
in the second page. In this case, CICS allocates another 2 buffers (3072 bytes) to minimize the
```
**138**   CICS TS for z/OS: System Initialization Parameter Reference


```
amount of unused storage. In this way, CICS uses storage that would otherwise be unavailable for
any other purpose.
decimal_value_2
The number of VSAM strings to be allocated for the use of intrapartition transient data. The value
must be in the range 1 through 255, and must not exceed the value specified in decimal_value_1.
The default value is 3.
For example, TD=(8,5) specifies 8 buffers and 5 strings.
The order in which you code the values is significant, so if you want to omit a value, you must code a
comma in the place of that value. For example, TD=(,2) specifies the default for the number of buffers
and explicitly specifies the number of strings.
```
### TDINTRA..................................................................................................................................................

```
The TDINTRA system initialization parameter specifies whether CICS is to initialize with empty
intrapartition TD queues.
TDINTRA={NOEMPTY|EMPTY}
Valid values are as follows:
NOEMPTY
CICS recovers all the intrapartition TD queues to the state they were in at the previous termination
of CICS, as in a normal emergency restart. The TD queue resource definitions are recovered from
the CICS global catalog.
EMPTY
CICS initializes with all the intrapartition TD queues empty. This option must be used when CICS is
initializing in remote site recovery mode (OFFSITE=YES).
You can optionally use this option to preform a cold start of your intrapartition TD queues to
initialize them as empty.
The option is significant only on warm and emergency restarts—cold starts always initialize with
empty queues. Note that the EMPTY option may cause data integrity problems because all indoubt
log records associated with logically recoverable TD queues are discarded.
The TD queue resource definitions are recovered from the CICS global catalog.
```
### TRANISO..................................................................................................................................................

```
The TRANISO system initialization parameter specifies, together with the STGPROT system initialization
parameter, whether you want transaction isolation in the CICS region.
TRANISO={NO|YES}
The permitted values are NO (the default), or YES.
NO
This is the default. If you specify NO, or allow this parameter to default, CICS operates without
transaction isolation, and all storage in the CICS address space is addressable. If you specify
STGPROT=YES and TRANISO=NO, CICS storage protection is active without transaction isolation.
YES
Transaction isolation is required. This ensures that the user-key task-lifetime storage of
transactions defined with the ISOLATE(YES) option is isolated from the user-key programs of
other transactions.
If you specify TRANISO=YES and STGPROT=YES, CICS operates with transaction isolation. YES is
the default for the STGPROT system initialization parameter.
If you specify TRANISO=YES, but STGPROT=NO is specified, CICS issues an information
message during initialization, and operates without transaction isolation. If STGPROT=NO and
TRANISO=YES are specified in the system initialization table, an error occurs during assembly
(MNOTE 8).
```
```
Chapter 1. System initialization parameter summary   139
```

```
Notes:
```
1. VSAM nonshared resources (NSR) are not supported for transactions that use transaction isolation.
    You should specify ISOLATE(NO) when you define transactions that access VSAM files using NSR.
    You can also function ship the file request to a remote region. The DFHMIRS program that carries
    out the request is defined with an EXECKEY of CICS. A CICS-key program has read and write
    access to CICS-key and user-key storage of its own task and all other tasks, whether or not
    transaction isolation is active.
2. Storage protection, transaction isolation, and command storage protection protect storage from
    user application code. They add no benefit to a region where no user code is executed; that is,
    a pure terminal-owning region (TOR) or a pure file-owning region (FOR) (where no distributed
    program link (DPL) requests are function-shipped).
3. Transaction isolation does not apply to 64-bit storage.
4. Transaction isolation does not apply to Java programs.
5. The JVM provides its own mechanisms that limit the risks which transaction isolation addresses.
    While ISOLATE(NO) can be specified for transactions that are running in a Liberty JVM server, the
    performance overheads are not removed. Managing the common subspace also imposes the cost
    of additional TCB switches from the T8 TCB running in Liberty to the QR TCB. Therefore, disabling
    transaction isolation is recommended.

### TRAP.........................................................................................................................................................

```
The TRAP system initialization parameter specifies whether the FE global trap exit is to be activated at
system initialization.
TRAP={OFF|ON}
This exit is for diagnostic use under the guidance of service personnel.
```
### TRDUMAX.................................................................................................................................................

```
The TRDUMAX system initialization parameter specifies the limit on the number of transaction dumps that
may be taken per dump table entry.
TRDUMAX={ 999 |number}
If this number is exceeded, subsequent transaction dumps for that particular entry will be
suppressed.
number
A number in the range 0 through 999. The default, 999, enables an unlimited number of dumps to
be taken.
For diagnostic guidance on dealing with incorrect dump output problems, see Dump output is incorrect.
```
### TRTABSZ..................................................................................................................................................

```
The TRTABSZ system initialization parameter specifies the size, in kilobytes, of the internal trace table.
TRTABSZ={ 12288 | number-of-kilobytes }
12288
The default size of the internal trace table is 12288 KB (12 MB).
number-of-kilobytes
The number of kilobytes of storage to be allocated for the internal trace table, in the range:
```
#### •

```
6.2
12288 KB (12 MB) through 1048576 KB (1 GB)
```
#### •

```
6.1
1024 KB through 1048576 KB (1 GB).
```
**140**   CICS TS for z/OS: System Initialization Parameter Reference


```
The table is page aligned and occupies a whole number of pages. If the value specified is not a
multiple of the page size (4 KB), it is rounded up to the next multiple of 4 KB.
The CICS internal trace table is allocated at an early stage during CICS initialization, and it exists for the
whole of the CICS run.
CICS obtains 64-bit z/OS storage (outside the CICS DSAs) for the internal trace table.
If you change the size of the internal trace table, check your current setting for the z/OS parameter
MEMLIMIT. MEMLIMIT limits the amount of 64-bit storage that the CICS address space can use. Your
setting for TRTABSZ must remain within MEMLIMIT , and you must also allow for other use of 64-bit
storage in the CICS region.
For information about the MEMLIMIT value for CICS, and instructions to check the value of MEMLIMIT
that currently applies to the CICS region, see Estimating and checking MEMLIMIT. For further information
about MEMLIMIT in z/OS, see Limiting the use of private memory objects in the z/OS MVS Programming:
Extended Addressability Guide.
```
### TRTRANSZ................................................................................................................................................

```
The TRTRANSZ system initialization parameter specifies the size, in kilobytes, of the transaction dump
trace table.
TRTRANSZ={ 1024 | number-of-kilobytes }
When a transaction dump is taken, CICS obtains storage from 64-bit z/OS storage for the transaction
dump trace table.
1024
1024 KB is the default size of the transaction dump trace table.
number-of-kilobytes
The number of kilobytes of storage to be allocated for the transaction dump trace table, in the
range 1024 KB through 1048576 KB (1 GB).
Trace entries are of variable lengths. The average length of a trace entry is approximately 100 bytes. 1
KB is equal to 1024 bytes.
When you set this parameter, check your current setting for the z/OS parameter MEMLIMIT.
MEMLIMIT limits the amount of 64-bit storage that the CICS address space can use. Your setting
for TRTRANSZ must remain within MEMLIMIT , and you must also allow for other facilities in the
CICS region that use 64-bit storage. See Estimating and checking MEMLIMIT. For information about
MEMLIMIT in z/OS, see Limiting the use of private memory objects in the z/OS MVS Programming:
Extended Addressability Guide.
```
### TRTRANTY................................................................................................................................................

```
The TRTRANTY system initialization parameter specifies which trace entries should be copied from the
internal trace table to the transaction dump trace table.
TRTRANTY={TRAN|ALL}
Valid values are as follows:
TRAN
Only the trace entries associated with the transaction that is abending will be copied to the
transaction dump trace table.
ALL
All of the trace entries from the internal trace table will be copied to the transaction dump trace
table. If the internal trace table size is larger than the transaction dump trace table size, the
transaction dump trace table could wrap. This results in only the most recent trace entries being
written to the transaction dump trace table.
```
```
Chapter 1. System initialization parameter summary   141
```

### TS.............................................................................................................................................................

```
The TS system initialization parameter specifies whether you want to perform a cold start for temporary
storage, as well as the number of VSAM buffers and strings to be used for auxiliary temporary storage.
TS=([COLD][,{0| 3 |decimal-value-1 }][,{ 3 |decimal-value-2}])
Valid values are as follows:
COLD
The type of start for the temporary storage facility. COLD forces a cold start regardless of the value
of the START parameter. If COLD is omitted, the TS start type is determined by the value of START.
0
No buffers are required; that is, only MAIN temporary storage is required.
decimal-value-1
The number of buffers to be allocated for the use of auxiliary temporary storage. The value must
be in the range 3 through 32 767.
decimal-value-2
The number of VSAM strings to be allocated for the use of auxiliary temporary storage. The value
must be in the range 1 through 255, and must not exceed the value specified in decimal-value-1.
The default value is 3.
For example, TS=(,8,5) specifies 8 buffers and 5 strings.
The operands of the TS parameter are positional. You must code commas to indicate missing
operands if others follow. For example, TS=(,8) specifies the number of buffers and allows the other
operands to default.
```
### TSMAINLIMIT..........................................................................................................................................

```
The TSMAINLIMIT system initialization parameter specifies a limit for the storage that is available for
main temporary storage queues to use. You can specify an amount of storage in the range 1 - 32768 MB
(32 GB), but this amount must not be greater than 25% of the value of the z/OS parameter MEMLIMIT.
The default is 64 MB.
TSMAINLIMIT={64M| nnnnn M| nn G}
64M
The default setting in megabytes.
nnnnn M
An amount of storage in megabytes. The allowed range is 1 - 32768 MB.
nn G
An amount of storage in gigabytes. The allowed range is 1 - 32 GB.
For example, TSMAINLIMIT=2G makes 2 GB of storage available to main temporary storage queues.
When you set this parameter, check your current setting for the z/OS parameter MEMLIMIT.
MEMLIMIT limits the amount of 64-bit storage that the CICS address space can use. Your setting
for TSMAINLIMIT must not be greater than 25% of the MEMLIMIT value.
If you set the TSMAINLIMIT system initialization parameter to greater than 25% of the MEMLIMIT
value, message DFHTS1608 is issued and CICS terminates.
For information about the MEMLIMIT value for CICS, and instructions to check the value of MEMLIMIT
that currently applies to the CICS region, see Estimating and checking MEMLIMIT. For further
information about MEMLIMIT in z/OS, see Limiting the use of private memory objects in the z/OS
MVS Programming: Extended Addressability Guide.
```
**142**   CICS TS for z/OS: System Initialization Parameter Reference


### TST...........................................................................................................................................................

```
The TST system initialization parameter specifies the temporary storage table suffix.
TST={NO|YES| xx }
NO
CICS uses only RDO support for temporary storage queues, and does not load a TST.
YES
CICS uses an unsuffixed version of the table, named DFHTST.
xx
CICS uses a table named DFHTST xx. See Defining CICS resource table and module keywords for
information on defining the temporary storage table suffix.
Note: To use a TST in combination with TSMODEL resource definitions, you must assemble the TST
load module with the MIGRATE option. If the TST is not assembled with the MIGRATE option, CICS
loads the TST only and does not provide any RDO support for temporary storage queues, and any
attempts to install TSMODEL resource definitions are rejected.
For information about coding the macros for this table, see Temporary storage table (TST).
```
### UDSASZE..................................................................................................................................................

```
The UDSASZE system initialization parameter specifies the size of the UDSA.
Important: Setting the size of individual dynamic storage areas (DSAs) is not usually necessary and it
is not recommended. If you specify DSA size values that, in combination, do not allow sufficient space
for the remaining DSAs, CICS fails to initialize. The limit on the storage available for the DSAs in 24-bit
storage (below the line) is specified by the DSALIM system initialization parameter system initialization
parameter. You must allow at least 256 KB for each DSA in 24-bit storage for which you have not set a
size. See DSALIM system initialization parameter.
UDSASZE={0K|number}
Valid values are as follows:The default size is 0, indicating that the DSA size can change dynamically. A
non-zero value indicates that the DSA size is fixed.
0 (zero)
The size of the UDSA dynamic storage area size can change dynamically. Zero is the default.
number
A non-zero value specifies that the size of the UDSA dynamic storage area is fixed.Specify number
as an amount of storage in the range 0 - 16777215 bytes in multiples of 262144 bytes (256 KB)..
If the size specified is not a multiple of 256 KB (or 1 MB if transaction isolation is active), CICS
rounds the value up to the next multiple. You can specify number as a number of bytes, a whole
number of kilobytes, or a whole number of megabytes. Use the letter M to indicate that the value
represents a whole number of megabytes (for example, 4 M). Use the letter K to indicate that the
value represents a whole number of kilobytes (for example, 4096 K), in which case the number is
rounded up to the number of megabytes.
Restriction: You can specify the UDSAZSE parameter in PARM, SYSIN, or CONSOLE only.
```
### UOWNETQL..............................................................................................................................................

```
The UOWNETQL system initialization parameter specifies a qualifier for the NETUOWID for units of work
initiated on the local CICS region.
UOWNETQL=user_defined_value
UOWNETQL is required only if the z/OS Communications Server VTAM=NO is coded. The specified
value is used in the following circumstances:
```
- CICS is performing a cold start and VTAM=NO has been specified.
- CICS is performing a cold start and the z/OS Communications Server ACB has failed to open.

```
Chapter 1. System initialization parameter summary   143
```

- CICS is being started with VTAM=NO and the z/OS Communications Server ACB has not been
    opened since the last cold start of CICS.
- CICS is being started, the z/OS Communications Server ACB has failed to open, and the z/OS
    Communications Server ACB has not been opened since the last cold start of CICS.
If any of the above conditions apply and UOWNETQL is not specified, a dummy default UOWNETQL
of 9UNKNOWN is used. This dummy UOWNETQL is invalid because the first character is a number.
UOWNETQL is given this invalid name to avoid a conflict with any real, valid netid.
If any of the above conditions apply, UOWNETQL, or its default value, is used as the IPIC NETWORKID
of this CICS region. It is also used as the default NETWORKID on IPCONN definitions for IPIC
connections to other CICS regions.
The value you code can be from 1 to 8 characters long, and must consist of uppercase letters (A
through Z), or numbers in the range 0 through 9. The first character must be a letter.

### USERTR....................................................................................................................................................

```
The USERTR system initialization parameter specifies whether the main user trace flag is to be set on or
off.
USERTR={ON|OFF}
If the user trace flag is off, the user trace facility is disabled, and EXEC CICS ENTER TRACENUM
commands receive an INVREQ condition if EXCEPTION is not specified. If the program does
not handle this condition, the transaction will abend with abend code AEIP. For programming
information about the user trace facility using EXEC CICS ENTER TRACENUM commands, see ENTER
TRACENUM.
When CICS is running, you can set the main user trace flag dynamically through the CETR transaction.
To learn about what user trace is and how user applications write custom trace entries to CICS trace data,
see User trace.
```
### USRDELAY................................................................................................................................................

```
The USRDELAY system initialization parameter specifies the maximum time, in the range 0 - 10080
minutes (up to seven days), that an eligible user ID and its associated attributes are cached in the CICS
region after use. A user ID that is retained in the user table can be reused.
USRDELAY={ 30 | number }
For a user ID to be retained in the CICS region and eligible for reuse in the USRDELAY period, one of
the following statements must apply to the user ID:
```
- The user ID was received from remote systems.
- The user ID was specified on the SECURITYNAME attribute in the CONNECTION resource.
- The user ID was specified on the USERID attribute in the SESSIONS resource.
- The user ID was specified on the USERID attribute in the definition of an intrapartition transient data
    queue.
- The user ID was specified on the USERID option on a START command.
- The user ID was specified on the USERID attribute for a non-terminal task, such as the alias tasks
    that are attached for processing HTTP requests.
Within the **USRDELAY** period, a user ID in any one of these categories can be reused in one of the
other categories, provided that the request for reuse has the same qualifiers. If a user ID is qualified
by a different group ID, APPLID, or terminal ID, a retained entry is not reused, except when changing
the terminal ID on LU6.2 when the retained entry is used.
If a user ID is unused for more than the **USRDELAY** limit, it is removed from the system, and the
message DFHUS0200 is issued. You can suppress this message in an XMEOUT global user exit
program.

**144**   CICS TS for z/OS: System Initialization Parameter Reference


```
If you specify USRDELAY=0 , all eligible user IDs are deleted immediately after use and cannot be
reused. With USRDELAY=0 set, the message DFHUS0200 is not issued.
When you specify USRDELAY=0 , CICS drives a full sign-on for each incoming request (with I/O to
RACF) and a full sign-off at the end of each transaction. This setting provides the highest level of
security, but in some scenarios performance might be a higher priority. For example, if the CICS region
communicates with other CICS regions and the connections carry high volumes of transaction routing
or function shipping activity, multiple instances of sign-on and sign-off might be required for a single
task. Select a USRDELAY value that gives the optimum balance of performance and security for the
type of work that is carried out in each CICS region.
When a value other than 0 is specified for USRDELAY , the user ID and its attributes are retained in
the region until the USRDELAY value has expired. For example, if you specified USRDELAY=30 for a
user ID, but that user ID continues to run transactions every 25 minutes, the USRDELAY value never
expires and any changes made to the user ID never come into effect.
Note: If RACFSYNC=YES , all cached user tokens for the user ID are flushed irrespective of the setting
of the USRDELAY parameter for that user ID. A type 71 ENF event occurs when a user ID is added or
removed from a group, or revoked. Learn more about RACFSYNC system initialization parameter.
If you previously specified low values for the USRDELAY system initialization parameter in your CICS
regions to ensure that CICS detected changes to RACF profiles quickly, you might want to increase
this value, because CICS is notified immediately if RACF profile changes occur. The primary impact of
a high USRDELAY value is that the amount of storage used for RACF control blocks is increased.
If you alter the RACF profile of a signed-on remote user, for example by revoking the user, CICS continues
to use the authorization established at the first attach request until one of the following situations occurs:
```
- The transaction performs a syncpoint.
- The attach request ends.
- Sign off occurs because RACF notifies CICS of changes to a user profile, and an attached request
    associated with that signed-on user ID completes, for all operands of ATTACHSEC except LOCAL.
- Sign off occurs because RACF notifies CICS of changes to a user profile, a new attach request is made,
    and the value in the **USRDELAY** system initialization parameter has not expired. This sign off is followed
    by a sign on.
**Tip:** The ISC/IRC attach time statistics of the DFHSTUP listing is for a CICS system using intersystem
communication or interregion communication. It provides summary statistics for the number of times that
the entries on the Persistent Verification "signed on from" list are either reused or timed out. Using this
data you can adjust the **USRDELAY** and **PVDELAY** system initialization parameters. For more information,
see ISC/IRC attach time entry statistics.

### USSCONFIG.............................................................................................................................................

```
The USSCONFIG system initialization parameter specifies the name and path of the root directory for CICS
Transaction Server configuration files on z/OS UNIX.
USSCONFIG={/var/cicsts/dfhconfig | directory }
Specifies the directory in which z/OS UNIX configuration files are stored. The default value is /var/
cicsts/dfhconfig.
The maximum length of the USSCONFIG system initialization parameter is 255 characters. Because
the USSCONFIG directory may have sub-directories, it is recommended that the maximum length of
the directory is 200.
Although the format of the USSCONFIG directory is the same as the USSHOME directory, they have
different purposes. USSHOME contains samples, USSCONFIG contains the customized versions of
these files, plus additional files. Some compliance regulations explicitly state that the default values
should not be used, but should be explicitly set. Therefore it is strongly recommended that you do not
set USSCONFIG to the USSHOME directory.
```
```
Chapter 1. System initialization parameter summary   145
```

### USSHOME.................................................................................................................................................

```
The USSHOME system initialization parameter specifies the name and path of the root directory for CICS
Transaction Server files on z/OS UNIX.
USSHOME={/usr/lpp/cicsts/cicsts62 | directory }
The value for the USSHOME system initialization parameter must match the directory that you
specified for CICS Transaction Server files on z/OS UNIX when you installed CICS using the DFHISTAR
installation job.
The default value for the USSHOME system initialization parameter matches the default value for the
DFHISTAR installation job: that is, /usr/lpp/cicsts/ cicsversion , where cicsversion is your
version of CICS:
```
#### •

```
6.2
/usr/lpp/cicsts/cicsts62
```
#### •

```
6.1
/usr/lpp/cicsts/cicsts61
The maximum length of the USSHOME system initialization parameter is 255 characters.
If you changed any of the TINDEX , PATHPREFIX , or USSDIR parameters in the DFHISTAR installation
job, you must specify a value for the USSHOME system initialization parameter to match the name and
path that you specified for the root directory using those DFHISTAR parameters.
```
### VTAM (z/OS Communications Server).....................................................................................................

```
The VTAM system initialization parameter specifies whether the z/OS Communications Server access
method is to be used.
ISC over SNA uses the ACF/Communications Server access method to provide the necessary protocols
to support communication between CICS regions that are in different z/OS images, or in different z/OS
sysplexes. For details, see Activating intersystem communication over z/OS Communications Server.
VTAM={YES|NO}
The default is VTAM=YES.
```
### VTPREFIX.................................................................................................................................................

```
The VTPREFIX system initialization parameter specifies the first character to be used for the terminal
identifiers (termids) of autoinstalled virtual terminals.
VTPREFIX={\| character }
Virtual terminals are used by the External Presentation Interface (EPI) and terminal emulator
functions of the CICS Client products.
Termids generated by CICS for autoinstalled Client terminals consist of a 1-character prefix and a
3-character suffix. The default prefix is '\'. The suffix can have the values 'AAA' through '999'. That
is, each character in the suffix can have the value 'A' through 'Z' or '0' through '9'. The first suffix
generated by CICS has the value 'AAA'. This is followed by 'AAB', 'AAC', ... 'AAZ', 'AA0', 'AA1', and so on,
up to '999'.
Each time a Client virtual terminal is autoinstalled, CICS generates a 3-character suffix that it has not
recorded as being in use.
By specifying a prefix, you can ensure that the termids of Client terminals autoinstalled on this
system are unique in your transaction routing network. This prevents the conflicts that could occur if
two or more terminal-owning regions (TORs) ship definitions of Client virtual terminals to the same
application-owning region (AOR).
If such a naming conflict does occur—that is, if a Client virtual terminal is shipped to an AOR on which
a remote terminal of the same name is already installed—the autoinstall user program is invoked in
the AOR. Your user program can resolve the conflict by allocating an alias terminal identifier to the
```
**146**   CICS TS for z/OS: System Initialization Parameter Reference


```
shipped definition. For details of writing an autoinstall user program to install shipped definitions,
see Writing a program to control autoinstall of shipped terminals. However, you can avoid potential
naming conflicts by specifying a different prefix, reserved for virtual terminals, on each TOR on which
Client virtual terminals are to be installed.
You must not use the characters + - * < > = { } or blank.
Note:
```
1. When specifying a prefix, ensure that termids generated by CICS for Client terminals do not conflict
    with those generated by your autoinstall user program for user terminals, or with the names of any
    other terminals or connections.
2. Client terminal definitions are not recovered after a restart. Immediately after a restart, no Client
    terminals are in use, so when CICS generates suffixes it begins again with 'AAA'. This means
    that CICS does **not** always generate the same termid for any given Client terminal. This in turn
    means that server applications should not assume that a particular CICS-generated termid always
    equates to a particular Client terminal.
    If your server programs do make this assumption, you can use your autoinstall user program to
    allocate alias termids, by which the virtual terminals will be known to CICS, in a consistent manner.
3. Clients can override CICS Transaction Server for z/OS-generated termids.

### WEBDELAY...............................................................................................................................................

```
The WEBDELAY system initialization parameter specifies two web delay periods, a timeout period and the
terminal keep time.
WEBDELAY=( 5 |time_out, 60 |keep_time)
A timeout period
The maximum time, in minutes, in the range 1-60, that a transaction started through the Web
3270 bridge interface, is allowed to remain in terminal wait state before it is automatically purged
by CICS.
The terminal keep time
The time, in minutes, in the range 1-6000, during which state data is kept for a CICS Web 3270
bridge transaction, before CICS performs clean-up.
For information about system initialization parameters that enable CICS web support, see Specifying
system initialization parameters for CICS web support.
```
### WLMHEALTH............................................................................................................................................

```
The WLMHEALTH system initialization parameter specifies the time interval and the health adjustment
value to be used by CICS on z/OS Workload Manager Health API (IWM4HLTH) calls, which CICS makes to
inform z/OS WLM about the health state of a CICS region.
WLMHEALTH={( 20 | interval [, 25 | number ])|OFF}]
interval
Specifies the amount of time, in seconds, between calls that CICS makes to the z/OS Workload
Manager Health API (IWM4HLTH). The value specified must be in the range 0 - 600. The default
value is 20.
number
Specifies the health adjustment value, as a percentage, that CICS provides to the z/OS Workload
Manager Health API (IWM4HLTH) in each call at the specified interval. The value must be in the
range 1 - 100. The default value is 25.
The health value is a number that shows, in percent, how well the server is performing. The
specified health adjustment value adjusts the health value of the region each time CICS invokes
the z/OS WLM Health API:
```
```
Chapter 1. System initialization parameter summary   147
```

- If the _interval_ value is 0, the initial z/OS WLM health value of the CICS region is set to 0 during
    CICS initialization, and the z/OS WLM health incrementing process must be initiated later by
    issuing a **SET WLMHEALTH OPEN** command or using a System policy rule.
- If the _interval_ value is greater than 0, the CICS server health value is incremented at the
    specified intervals. The first interval starts when the following message is issued:
    DFHSI1517 applid Control is being given to CICS
    For example, WLMHEALTH=(5,10) specifies that CICS updates the z/OS WLM health value in
    increments of 10 every 5 seconds until the health value reaches 100.
The z/OS WLM health value is set to 0 during the CICS shutdown process, regardless of the
current z/OS WLM health value.
**OFF**
Specifies that CICS does not use the z/OS Workload Manager Health API (IWM4HLTH) to inform
z/OS WLM about the health state of a CICS address space.
To use the WLM health settings that are provided by CICS, the z/OS TCP/IP stack needs to be
configured to use a value of SERVERWLM for the **VIPADISTRIBUTE DISTMETHOD** or SHAREPORTWLM
on the PORT statement. In this case, if the health value for a CICS region is less than 100, z/OS WLM
reduces the recommendation that is provided to TCP/IP for that region. For more information, see z/OS
Communications Server: IP Configuration Reference and z/OS Communications Server: IP Configuration
Guide.
If you change the **WLMHEALTH** value while CICS is running, the change is cataloged in the local catalog.
If **WLMHEALTH** is specified in the system initialization table, the cataloged value that is specified by the
change overrides the value of the **WLMHEALTH** system initialization parameter on an initial or cold restart.
The cataloged value is not used if you specify **WLMHEALTH** as a system initialization parameter override
(for example, in SYSIN), or if you reinitialize the CICS catalog data sets.
A change to the value for the **WLMHEALTH** interval or health adjustment is cataloged in the local catalog,
so it takes precedence on subsequent AUTO restarts of CICS and prevents an interval value of zero
being used. You might want to specify the **WLMHEALTH** interval value as zero on startup (for example,
WLMHEALTH=(0,25) ), and then modify the setting after control is given to CICS and when the region is
deemed fully ready to process work. Specifying **WLMHEALTH** as a system initialization parameter override
allows you to get this desired behavior.

### WRKAREA................................................................................................................................................

```
The WRKAREA system initialization parameter specifies the number of bytes to be allocated to the
common work area (CWA). The CWA is one of the facilities that CICS provides for sharing data across
transactions. Data stored in the CWA is available to any transaction in the system. Subject to resource
security and storage protection restrictions, any transaction can write to them and any transaction can
read them.
WRKAREA={ 512 |number}
This area, for use by your installation, is initially set to binary zeros, and is available to all programs. It
is not used by CICS. The maximum size for the work area is 3584 bytes.
```
### XAPPC......................................................................................................................................................

```
The XAPPC system initialization parameter specifies whether RACF session security can be used when
establishing APPC sessions.
XAPPC={NO|YES}
Valid values are as follows:
NO
RACF session security cannot be used.
YES
RACF session security can be used.
```
**148**   CICS TS for z/OS: System Initialization Parameter Reference


```
If you specify BINDSECURITY=YES for a specific APPC connection, a request to RACF is issued to
extract the security profile. If the profile exists, it is used to bind the session.
Note: If you specify XAPPC=YES, the external security manager that you use must support the
APPCLU general resource class, otherwise CICS fails to initialize.
Restriction: You can specify the XAPPC parameter in the SIT, PARM, or SYSIN only.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### XCFGROUP...............................................................................................................................................

```
The XCFGROUP system initialization parameter specifies the name of the cross-system coupling facility
(XCF) group to be joined by this region.
XCFGROUP={DFHIR000| name }
The group name must be eight characters long, padded at the end with blanks if necessary. The
valid characters are A-Z 0-9 and the national characters $ # and @. To avoid using the names IBM
uses for its XCF groups, do not begin group names with the letters A through C, E through I, or the
character string "SYS". Also, do not use the name "UNDESIG", which is reserved for use by the system
programmer in your installation.
It is recommended that you use a group name beginning with the letters "DFHIR".
You can specify XCFGROUP on the SIT macro or as a SYSIN override. You cannot specify it as a console
override.
Each CICS region can join only one XCF group, which happens when it signs on to CICS interregion
communication (IRC). The default XCF group is DFHIR000.
XCF groups allow CICS regions in different MVS images within the same sysplex to communicate with
each other across multi-region operation (MRO) connections.
Note: Regions in the same MVS image too, can communicate with each other using MRO, but this does
not require a coupling facility. The only situation in which CICS regions in the same MVS image cannot
communicate via MRO is when they are members of different XCF groups. EXCI applications and
target CICS regions must also use the same XCFGROUP. If they do not, you must code a DFHXCOPT
table with a XCFGROUP equal to the XCFGROUP coded within the SIT of the target CICS region.
You must also ensure the new DFHXCOPT table is placed within a data set that resides above the
SDFHEXCI data set.
For introductory information about XCF/MRO, and instructions on how to set up XCF groups, see
Cross-system multiregion operation (XCF/MRO).
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### XCMD........................................................................................................................................................

```
The XCMD system initialization parameter specifies whether you want CICS to perform command security
checking, and optionally the RACF resource class name in which you have defined the command security
profiles.
XCMD={YES|name|NO}
If you specify YES, or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a transaction is authorized to use a CICS command for the specified resource. Such
checking is performed every time a transaction tries to use a COLLECT, DISABLE, DISCARD, ENABLE,
EXTRACT, INQUIRE, PERFORM, RESYNC, or SET command, or any of the FEPI commands, for a
resource.
Note: The checking is performed only if you have specified YES for the SEC system initialization
parameter and specified the CMDSEC(YES) option on the transaction resource definition.
```
```
Chapter 1. System initialization parameter summary   149
```

#### YES

```
CICS calls RACF, using the default class name of CICSCMD prefixed by C or V, to check whether
the user ID associated with a transaction is authorized to use a CICS command for the specified
resource. The general resource class name is CCICSCMD and the resource group class name is
VCICSCMD.
name
CICS calls RACF, using the specified resource class name prefixed by C or V, to verify that the user
ID associated with a transaction is authorized to use a CICS command for the specified resource.
The general resource class name is C name and the resource group class name is V name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any command security checks, allowing any user to use commands that
would be subject to those checks.
Restrictions: You can specify the XCMD parameter in the SIT, PARM, or SYSIN only.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### XDB2........................................................................................................................................................

```
The XDB2 system initialization parameter specifies whether you want CICS to perform DB2ENTRY security
checking.
XDB2={NO|name}
Valid values are as follows:
NO
CICS does not perform any Db2 resource security checks.
name
CICS calls RACF, using the specified general resource class name, to check whether the user ID
associated with the CICS Db2 transaction is authorized to access the DB2ENTRY referenced by
the transaction.
Unlike the other Xnnn system initialization parameters, this Db2 security parameter does not
provide a YES option that implies a default CICS resource class name for DB2ENTRY resources.
You have to specify your own Db2 resource class name.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### XDCT.........................................................................................................................................................

```
The XDCT system initialization parameter specifies whether you want CICS to perform resource security
checking for transient data queues.
XDCT={YES|name|NO}
If you specify YES or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a transaction is authorized to access the transient data queue. Such checking is
performed every time a transaction tries to access a transient data queue.
Note: The checking is performed only if you have specified the SEC=YES system initialization
parameter and the RESSEC(YES) option in the transaction resource definition. For information on
how resource security can provide a further level of security to transaction security, see Resource
security.
YES
CICS calls RACF, with the default CICS resource class name of CICSDCT prefixed by D or E, to
verify whether the user ID associated with the transaction is authorized to access the specified
transient data queue.
```
**150**   CICS TS for z/OS: System Initialization Parameter Reference


```
The general resource class name is DCICSDCT and the resource group class name is ECICSDCT.
name
CICS calls RACF, using the specified resource class name, to check whether the user ID
associated with the transaction is authorized to access the specified transient data queue. The
general resource class name is D name and the resource group class name is E name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any transient data security checks, allowing any user to access any
transient data queue.
Restriction: You can specify the XDCT parameter in the SIT, PARM, or SYSIN only.
```
### XFCT.........................................................................................................................................................

```
The XFCT system initialization parameter specifies whether you want CICS to perform file resource
security checking, and optionally specifies the RACF resource class name in which you have defined the
file resource security profiles.
XFCT={YES|name|NO}
If you specify YES, or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a transaction is authorized to access File Control-managed files. Such checking
is performed every time a transaction tries to access a file managed by CICS file control. The
checking is performed only if you have specified the SEC=YES system initialization parameter and
the RESSEC(YES) option in the resource definitions. For information on how resource security can
provide a further level of security to transaction security, see Resource security.
Note: You can specify the XFCT parameter in the SIT, PARM, or SYSIN only.
YES
CICS calls RACF, using the default CICS resource class name of CICSFCT prefixed by F or H, to
verify that the user ID associated with a transaction is authorized to access files reference by the
transaction. The general resource class name is FCICSFCT and the resource group class name is
HCICSFCT.
name
CICS calls RACF, using the specified resource class name, to verify that the user ID associated
with a transaction is authorized to access files referenced by the transaction. The general resource
class name is F name and the resource group class name is H name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any file resource security checks, allowing any user to access any file.
```
### XHFS.........................................................................................................................................................

```
The XHFS system initialization parameter specifies whether CICS is to check the transaction user's ability
to access files in the z/OS UNIX System Services file system.
XHFS={YES|NO}
At present, this checking applies only to the user ID of the Web client when CICS Web support is
returning z/OS UNIX file data as the static content identified by a URIMAP definition. The checking
is performed only if you have specified the SEC=YES system initialization parameter. However, the
RESSEC option in the transaction resource definition does not affect this security checking. For
information on how resource security can provide a further level of security to transaction security,
see Resource security.
Note: You can specify the XHFS parameter in the SIT, PARM, or SYSIN only.
```
```
Chapter 1. System initialization parameter summary   151
```

#### YES

```
CICS is to check whether the user identified as the Web client is authorized to access the file
identified by the URIMAP that matches the incoming URL. This check is in addition to the check
performed by z/OS UNIX System Services against the CICS region user ID. If access to the file is
denied for either of these user IDs, the HTTP request is rejected with a 403 (Forbidden) response.
NO
CICS is not to check the client user's access to z/OS UNIX files. Note that the CICS region user
ID's access to these files is still checked by z/OS UNIX System Services.
```
### XJCT.........................................................................................................................................................

```
The XJCT system initialization parameter specifies whether you want CICS to perform journal resource
security checking.
XJCT={YES|name|NO}
If you specify YES, or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a transaction is authorized to access the referenced journal. Such checking is
performed every time a transaction tries to access a CICS journal. The checking is performed only
if you have specified the SEC=YES system initialization parameter and the RESSEC(YES)in the
resource definitions. For information on how resource security can provide a further level of security
to transaction security, see Resource security.
Note: You can specify the XJCT parameter in the SIT, PARM, or SYSIN only.
YES
CICS calls RACF using the default CICS resource class name of CICSJCT prefixed by a J or K, to
check whether the user ID associated with a transaction is authorized to access CICS journals
referenced by the transaction. The general resource class name is JCICSJCT and the resource
group class name is KCICSJCT.
name
CICS calls RACF, using the specified resource class name prefixed by J or K, to verify that the user
ID associated with a transaction is authorized to access CICS journals. The general resource class
name is J name and the resource group class name is K name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any journal resource security checks, allowing any user to access any CICS
journal.
```
### XLT............................................................................................................................................................

```
The XLT system initialization parameter specifies a suffix for the transaction list table.
XLT={NO|xx|YES}
The table contains a list of transactions that can be attached during the first quiesce stage of system
termination. See Defining CICS resource table and module keywords.
YES
The default transaction list table, DFHXLT, is used.
xx
The transaction list table DFHXLTxx is used.
NO
A transaction list table is not used.
For guidance information about coding the macros for this table, see Transaction list table (XLT).
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
**152**   CICS TS for z/OS: System Initialization Parameter Reference


### XPCT.........................................................................................................................................................

```
The XPCT system initialization parameter specifies whether you want CICS to perform started transaction
resource security checking, and optionally specifies the name of the RACF resource class name in which
you have defined the started task security profiles.
XPCT={YES|name|NO}
If you specify YES, or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a transaction is authorized to use started transactions and related EXEC CICS
commands. Such checking is performed every time a transaction tries to use a started transaction or
one of the EXEC CICS commands: COLLECT STATISTICS TRANSACTION, DISCARD TRANSACTION,
INQUIRE TRANSACTION, or SET TRANSACTION. The checking is performed only if you have specified
the SEC=YES system initialization parameter and the RESSEC(YES) option in the resource definitions.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
Note: You can specify the XPCT parameter in the SIT, PARM, or SYSIN only.
YES
CICS calls RACF using the default CICS resource class name CICSPCT prefixed with A or B, to
verify that the user ID associated with a transaction is authorized to use started transactions or
related EXEC CICS commands.
The general resource class name is ACICSPCT and the resource group class name is BCICSPCT.
name
CICS calls RACF, using the specified resource class name, to verify that the user ID associated
with a transaction is authorized to use started transactions or related EXEC CICS commands. The
general resource class name is A name and the resource group class name is B name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any started task resource security checks, allowing any user to use started
transactions or related EXEC CICS commands.
```
### XPPT.........................................................................................................................................................

```
The XPPT system initialization parameter specifies that CICS is to perform application program resource
security checks and optionally specifies the RACF resource class name in which you have defined the
program resource security profiles.
XPPT=({YES| class_name |NO}[,{ALL|DPLONLY}])
You can specify the XPPT parameter in the SIT, PARM, or SYSIN only. Checking is performed every
time a transaction tries to invoke another program by using one of the CICS commands: LINK, LOAD,
or XCTL.
Note: The security check is performed only if you have specified the SEC=YES system initialization
parameter and the RESSEC(YES) option in the resource definitions. For information on how resource
security can provide a further level of security to transaction security, see Resource security.
YES
CICS calls RACF, using the default resource class name prefixed by M or N, to verify that the user
ID associated with a transaction is authorized to use LINK, LOAD, or XCTL commands to invoke
other programs. The general resource class name is MCICSPPT and the resource group class
name is NCICSPPT.
class_name
CICS calls RACF, with the specified resource class name prefixed by M or N, to verify that the user
ID associated with a transaction is authorized to use LINK, LOAD, or XCTL commands to invoke
other programs. The general resource class name is M class_name and the resource group class
name is N class_name.
```
```
Chapter 1. System initialization parameter summary   153
```

```
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any application program authority checks, allowing any user to use LINK,
LOAD, or XCTL commands to invoke other programs. It overrides the ALL or DPLONLY option.
```
```
6.2
ALL
Performs the security check on all programs invoked by LINK, LOAD, or XCTL commands. It works
only when YES or class_name is specified. It is overridden by the NO option.
```
```
6.2
DPLONLY
Performs the security check only on the first program that is linked by the mirror program during
distributed program link (DPL). It works only when YES or class_name is specified. It is overridden
by the NO option.
```
### XPSB.........................................................................................................................................................

```
The XPSB system initialization parameter specifies whether you want CICS to perform program
specification block (PSB) security checking and optionally specifies the RACF resource class name in
which you have defined the PSB security profiles.
XPSB={YES|name|NO}
You can specify the XPSB parameter in the SIT, PARM, or SYSIN only. If you specify YES, or a RACF
resource class name, CICS calls RACF to check that the user ID associated with a transaction is
authorized to access PSBs (which describe databases and logical message destinations used by
application programs). Such checking is performed every time a transaction tries to access a PSB.
Note:
```
1. The checking is performed only if you have specified the **SEC=YES** system initialization parameter
    and the RESSEC(YES) option on the resource definitions. For further information on how resource
    security can provide a further level of security to transaction security, see Resource security.
2. If you require security checking for PSBs to apply to remote users who access this region by means
    of transaction routing, the system initialization parameter **PSBCHK** =YES must be specified. For
    more information about this parameter, see “PSBCHK” on page 105.
**YES**
CICS calls RACF, using the default resource class name CICSPSB prefixed by P or Q, to verify that
the user ID associated with a transaction is authorized to access PSBs. The general resource class
name is PCICSPSB and the resource group class name is QCICSPSB.
**name**
CICS calls RACF, using the specified resource class name prefixed by P or Q, to verify that the user
ID associated with a transaction is authorized to access PSBs. The general resource class name is
P _name_ and the resource group class name is Q _name_.
The resource class name specified must be 1 through 7 characters.
**NO**
CICS does not perform any PSB resource security checks, allowing any user to access any PSB.

### XPTKT.......................................................................................................................................................

```
The XPTKT system initialization parameter specifies whether CICS checks if a user can generate a
PassTicket for the user's userid using the EXEC CICS REQUEST PASSTICKET command, the EXEC
CICS REQUEST ENCRYPTPTKT command, or the EXEC FEPI REQUEST PASSTICKET command.
You can specify the XPTKT parameter in the SIT, PARM, or SYSIN only.
For information about PassTickets, see How it works: PassTickets.
```
**154**   CICS TS for z/OS: System Initialization Parameter Reference


#### XPTKT={YES|NO}

```
Valid values for this parameter are as follows:
YES
A check is made that the userid has update authority for the profile
IRRPTAUTH.applid.userid in the class PTKTDATA.
NO
No check is done.
```
### XRES.........................................................................................................................................................

```
The XRES system initialization parameter specifies whether you want CICS to perform resource security
checking for particular CICS resources and optionally specifies the resource class name in which you have
defined the resource security profiles.
XRES={YES| name |NO}
You can specify the XRES parameter in the SIT, PARM, or SYSIN only. If you specify YES, or a general
resource class name, CICS calls RACF to verify that the user ID associated with a transaction is
authorized to use the resource. This checking is performed every time a transaction tries to access a
resource.
The actual profile name passed to RACF is the name of the resource to be checked, prefixed
by its resource type; for example, for a document template whose resource definition is named
“WELCOME", the profile name passed to RACF is DOCTEMPLATE.WELCOME. Even if a command
references the document template using its 48-character template name, the shorter name (up to 8
characters) of the DOCTEMPLATE resource definition is always used for security checking.
The checking is performed only if the SEC=YES system initialization parameter is in use and the
RESSEC(YES) option is specified in the TRANSACTION resource definition. For information on how
resource security can provide a further level of security to transaction security, see Resource security.
YES
CICS calls RACF, using the default CICS resource class name of RCICSRES, to check whether the
user ID associated with a transaction is authorized to use the resource it is trying to access. The
general resource class name is RCICSRES and the resource group class name is WCICSRES.
name
CICS calls RACF, using the specified resource class name prefixed by the letter R, to check
whether the user ID associated with a transaction is authorized to use the resource it is trying to
access. The general resource class name is R name and the resource group class name is W name.
The resource class name specified must be 1 through 7 characters.
NO
CICS does not perform any security checks for resources, allowing access to any user.
For a list of commands subject to XRES resource class checks, together with their respective profiles, see
Resource and command check cross reference.
```
### XRF...........................................................................................................................................................

```
Stabilized feature: The Extended Recovery Facility (XRF) in CICS is stabilized. Consider alternative
technologies that provide more flexible high-availability solutions for modern workloads. These solutions
include the z/OS Automatic Restart Manager (ARM), CICS data sharing, VTAM persistent sessions, and use
of the cross-system coupling facility. See also Stabilization notices.
The XRF system initialization parameter specifies whether XRF support is to be included in the CICS
region.
XRF={NO|YES} (active and alternate)
If the CICS region is started with the START=STANDBY system initialization parameter specified,
the CICS region is the alternate CICS region. If the CICS region is started with the START=AUTO,
```
```
Chapter 1. System initialization parameter summary   155
```

```
START=INITIAL or START=COLD system initialization parameter specified, the CICS region is the
active CICS region. The active CICS region signs on as such to the CICS availability manager.
If you specify XRF=YES, do not specify a value for the GRNAME system initialization parameter. Any
value specified is set to blanks.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
Note: Use of GNTRAN option DISCARD is not supported with XRF=YES.
```
### XTRAN......................................................................................................................................................

```
The XTRAN system initialization parameter specifies whether you want CICS to perform transaction
security checking and optionally specifies the RACF resource class names in which you have defined the
transaction security profiles.
XTRAN={YES| name |NO}
You can specify the XTRAN parameter in the SIT, PARM, or SYSIN only. If you specify YES, or a RACF
resource class name, CICS calls RACF to verify that the user ID associated with the transaction is
permitted to run the transaction.
Note: The checking is performed only if you have specified YES for the SEC system initialization
parameter.
YES
CICS calls RACF, using the default CICS resource class name of CICSTRN prefixed by T or G, to
verify that the user ID associated with the transaction is authorized to run the transaction. The
general resource class name is TCICSTRN and the resource group class name is GCICSTRN.
name
CICS calls RACF, using the specified resource class name prefixed by T or G, to verify that the user
ID associated with the transaction is authorized to run the transaction. The general resource class
name is T name and the corresponding resource group class name is G name.
The name specified must be 1 through 7 characters.
NO
CICS does not perform any transaction security checks, allowing any user to run any transaction.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### XTST.........................................................................................................................................................

```
The XTST system initialization parameter specifies whether you want CICS to perform security checking
for temporary storage queues and optionally specifies the RACF resource class name in which you have
defined the temporary storage security profiles.
XTST={YES|name|NO}
If you specify YES, or a RACF resource class name, CICS calls RACF to verify that the user ID
associated with a temporary storage request is authorized to access the referenced temporary storage
queue.
Note: You can specify the XTST parameter in the SIT, PARM, or SYSIN only.
Security checking for temporary storage queues is performed only if all of the following options are
specified in addition to the XTST parameter:
```
- The **SEC=YES** system initialization parameter
- RESSEC(YES) in the relevant TRANSACTION resource definitions
- SECURITY(YES) in your TSMODEL resource definitions
- If you use a temporary storage table (TST), the DFHTST TYPE=SECURITY macro

**156**   CICS TS for z/OS: System Initialization Parameter Reference


```
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
YES
CICS calls RACF, using the default CICS resource class name of CICSTST prefixed by S or U, to
verify that the user ID associated with the transaction is authorized to access temporary storage
queues referenced by the transaction. The general resource class name is SCICSTST and the
corresponding resource group class name is UCICSTST.
name
CICS calls RACF, using the specified resource class name prefixed by S or U, to verify that the user
ID associated with a transaction is authorized to access temporary storage queues. The general
resource class name is S name and the resource group class name is U name.
The name specified must be 1 through 7 characters.
NO
CICS does not perform any temporary storage security checks, allowing any user to access any
temporary storage queue.
```
### XUSER......................................................................................................................................................

```
The XUSER system initialization parameter specifies whether CICS is to perform surrogate user checks.
XUSER={YES|NO}
You can specify the XUSER parameter in the SIT, PARM, or SYSIN only. Valid values are as follows:
YES
CICS is to perform surrogate user checking in all those situations that permit such checks to be
made; for example, on EXEC CICS START commands without an associated terminal. Surrogate
user security checking is also performed by CICS against user IDs installing or modifying Db2
resource definitions that specify AUTHID or COMAUTHID.
Note: The XUSER parameter is also used by CICS to control access to the AUTHTYPE and
COMAUTHTYPE attributes on Db2 resource definitions, although not through surrogate user
checks. For more information about AUTHTYPE and COMAUTHTYPE attributes, see DB2CONN
resources.
For information about the various circumstances in which CICS performs surrogate user checks,
see Surrogate security.
NO
CICS is not to perform any surrogate user checking.
For information on how resource security can provide a further level of security to transaction security,
see Resource security.
```
### ZOSMONINTERVAL..................................................................................................................................

```
6.2
Applies to 6.2.
The ZOSMONINTERVAL system initialization parameter specifies the sampling interval, in seconds, for the
CICS z/OS storage monitor task.
The CICS z/OS storage monitor checks on unallocated storage in the z/OS user region storage, extended
user region storage, and MEMLIMIT storage. If a significant change in the amount of unallocated z/OS
storage occurs, the monitor issues console messages. In a short-on-storage (SOS) situation, the CICS
z/OS storage monitor might dynamically change the monitoring interval to allow closer monitoring of the
situation.
For more information about CICS monitoring of unallocated z/OS storage, see Monitoring unallocated
z/OS storage for CICS.
```
```
Chapter 1. System initialization parameter summary   157
```

```
ZOSMONINTERVAL={ 60 | number-of-seconds }
The default is 60.
number-of-seconds
Specifies the monitor sampling interval, in seconds, for the CICS z/OS storage monitor. The value
must be in the range in the range 1 - 60.
```
### ZOSSOSNEWTCB.....................................................................................................................................

```
6.2
Applies to 6.2.
The ZOSSOSNEWTCB system initialization parameter specifies the action that CICS takes in response to a
new open TCB that is being attached directly by CICS when the z/OS user region storage or extended user
region storage is short on storage (SOS). These open TCBs are L8, L9, X8 and X9 TCBs.
ZOSSOSNEWTCB={DELAY|NODELAY}
The values are as follows:
DELAY
This is the default. In SOS situations, the transaction that requires a new open TCB being attached
directly by CICS is delayed until neither the user region storage nor the extended user region
storage is in SOS conditions, or until the transaction times out or is purged.
Transactions that are delayed are suspended on a resource type of MVS_Stor with a resource
name of stor_constraint.
When ZOSSOSNEWTCB=DELAY is in effect, other CICS domains are notified of the SOS condition. If
possible, the notified domains try to alleviate the situation.
NODELAY
The attach of these TCBs is not delayed.
```
### ZOSSOS24UNALLOC................................................................................................................................

```
6.2
Applies to 6.2.
The ZOSSOS24UNALLOC system initialization parameter specifies short-on-storage (SOS) thresholds in
KB for the total amount of unallocated z/OS user region storage and for the largest contiguous storage
area available in it.
CICS considers the z/OS user region storage in the 24-bit addressing range to be SOS if the total amount
of unallocated storage or the size of the largest contiguous storage area available in it is less than or equal
to its threshold value.
ZOSSOS24UNALLOC=({ 64 | number-of-kilobytes1 [, 32 | number-of-kilobytes2 ]})
The default is ZOSSOS24UNALLOC=(64,32), which means that the user region storage is SOS if either
of the following situations occurs:
```
- The total amount of unallocated user region storage is less than or equal to 64 KB.
- The size of the largest contiguous storage area available in unallocated user region storage is less
    than or equal to 32 KB.
The order in which you code the values is significant. If you want to omit a value, you must code
a comma in the place of that value. For example, ZOSSOS24UNALLOC=(,16) specifies the default
threshold for the total amount of unallocated user region storage and a threshold of 16 KB for the
largest contiguous storage area available in it.
**_number-of-kilobytes1_**
    The SOS threshold for the total amount of unallocated user region storage.
    Specify a value in KB in the range 1 through 1024. The default is 64.

**158**   CICS TS for z/OS: System Initialization Parameter Reference


```
number-of-kilobytes2
The SOS threshold for the largest contiguous storage area available in unallocated user region
storage.
Specify a value in KB in the range 1 through 1024, and the value must not be greater than
number-of-kilobytes1.
The default is 32; however, if number-of-kilobytes1 is less than 32, the
default is number-of-kilobytes1. For example, ZOSSOS24UNALLOC=(48,) is equivalent
to ZOSSOS24UNALLOC=(48,32), but ZOSSOS24UNALLOC=(24,) is equivalent to
ZOSSOS24UNALLOC=(24,24).
```
### ZOSSOS31UNALLOC................................................................................................................................

```
6.2
Applies to 6.2.
The ZOSSOS31UNALLOC system initialization parameter specifies short-on-storage (SOS) thresholds in
KB for the total amount of unallocated z/OS extended user region storage and for the largest contiguous
storage area available in it.
CICS considers the z/OS extended user region storage in the 31-bit addressing range to be SOS if the total
amount of unallocated storage or the size of the largest contiguous storage area available in it is less than
or equal to its threshold value.
ZOSSOS31UNALLOC=({ 128 | number-of-kilobytes1 [, 64 | number-of-kilobytes2 ]})
The default is ZOSSOS31UNALLOC=(128,64), which means that the extended user region storage is
SOS if either of the following situations occurs:
```
- The total amount of unallocated extended user region storage is less than or equal to 128 KB.
- The largest contiguous storage area available in unallocated extended user region storage is less
    than or equal to 64 KB.
The order in which you code the values is significant. If you want to omit a value, you must code
a comma in the place of that value. For example, ZOSSOS31UNALLOC=(,32) specifies the default
threshold for the total amount of unallocated extended user region storage and a threshold of 32 KB
for the largest contiguous storage area available in it.
**_number-of-kilobytes1_**
    The SOS threshold for the total amount of unallocated extended user region storage.
    Specify a value in KB in the range 1 through 16384. The default is 128.
**_number-of-kilobytes2_**
    The SOS threshold for the largest contiguous storage area available in unallocated extended user
    region storage.
    Specify a value in KB in the range 1 through 16384, and the value must not be greater than
    _number-of-kilobytes1_.
    The default is 64; however, if _number-of-kilobytes1_ is less than 64, the
    default is _number-of-kilobytes1_. For example, ZOSSOS31UNALLOC=(160,) is equivalent
    to ZOSSOS31UNALLOC=(160,64), but ZOSSOS31UNALLOC=(32,) is equivalent to
    ZOSSOS31UNALLOC=(32,32).

### ZOSSOS64UNALLOC................................................................................................................................

```
6.2
Applies to 6.2.
The ZOSSOS64UNALLOC system initialization parameter specifies a short-on-storage (SOS) threshold in
MB for the amount of unallocated z/OS MEMLIMIT storage in the 64-bit addressing range.
CICS considers the z/OS MEMLIMIT storage in the 64-bit addressing range to be SOS if the total amount
of unallocated MEMLIMIT storage is less than or equal to the threshold value.
```
```
Chapter 1. System initialization parameter summary   159
```

```
ZOSSOS64UNALLOC={ 64 | number-of-megabytes }
number-of-megabytes
Specify a value in MB in the range 1 through 2048. The default is 64.
```