# Requirement Specifications

## General Description
Currently, the attendance check for each course at the DHBW Friedrichshafen is carried out via a written list of participants. Each student must sign the relevant line. The completed lists are then sent to the secretary's office by designated students. As soon as all lists have been received, each list is checked manually for completeness.

This is precisely the process we are addressing with the development of our full-stack application. The application's goal is to support the secretary's office by checking the "participant lists" automatically. All signatures on the participant lists are analyzed, and the user is provided with an overview of attendance. In addition, the user is given the opportunity to intervene directly in exceptional cases, as well as a statistical overview of attendance using a database. 

## Customer requirements
- Ease of use
   - Settings Page
   - User Documentation: "Help in program"
- Performance
   - Should not influence normal system operation
- Runs locally
- Reliability
   - Image processing should have a GOOD??? accuracy
   - Edge Cases should be displayed for the user to decide
- Mail Integration
- Automatic background processing
- Statistics
  - UI
- OpenSource License
- GDPR/DSGVO Compliance
- The secretary's office- Mrs. Schmidt says:
   - Show list and visualize missing names + return missing names
   - Highlight data of professor, room number and date
- IMAP/SMTP(?)


## Optional Features
- Dualis Integration
- Advertisement
  - Video
- Project Website (GitHub Pages)
- Welcome Page
 
## Specialized environment
- Fullstack development
- Image processing
- Security of sensitive data
- GDPR/DSGVO
  
## Usage & Outlook
As already indicated, the application will initially be used in the secretariat of the DHBW Friedrichshafen. This should reduce the workload on the staff by automating the time-consuming, manual checking of the "participant lists". This will free up capacities and allow the staff to focus on more important tasks.

In the future, with the approval of the DHBW, the current programme could be extended to include authentic signature recognition, which would be able to check signatures for correctness. With this extension, the DHBW could extend signature verification to all other DHBW locations, thus providing far-reaching workload reduction.

-----
Back to main page [here](https://github.com/DHBW-SE-2023/Wiki/blob/main/README.md).

# Product description

## GUI
A user hast o be able to navigate from every view to every other view via some way. There does not need to be a direct way in the navigation menu.
## Overview
The GUI consists of a main view containing an overview over the different courses with statistics of the current day. If there are no statistics for the current day, then show the latest statistics.
The overview contains a list showing every course. It gives the viewer a clear impression of what course it is. It does that by showing the full name of the course along with its short form (e.g. something like „Intelligente Systeme (TIK)“. 
For every course it also displays the number of present and absent students. The colour for displaying the number of missing students should be slightly highlighted in comparison to the number of present students.
It should also contain a button to export the list of students that are present and absent for every course. A similar button should be available to export the lists for all courses or a subset of courses. There have to be multiple options to export. Pressing the button executes a default action, but there is also a small menu to execute a different export action. The same menu should be able to change the default action.
This overview acts also as a to-do list for the secretariat. All unhandled evaluations of the attendence sheets are marked in the course list. An unhandled evaluation happens when the program evaluates a list but is unsure wether a student is signature field on the attendence sheet is valid or not. Entries that are marked, don’t update to show the latest statistics, they remain as they are. They are pushed to the bottom of the list, and a new entry with the latest statistics appears in their place. There is also an indicator that shows if there are entries that are marked as unhandled evaluations. When an unhandled evalutation is resolved the marked entry disappears from the list.
When clicking on a course element in the overview list a seperate view giving more detailed statistics and information about the course.
## Course View
This view gives more detailed information about the course. It provides both current and historic data about the course. It contains a list of all students that were and are missing together with the date. One should be able to view in a graph or a list, all students that are missing, present or a combinded dataset of the two options, or a subset of any of those.
## Student View
There is also a seperate subview, which displays the students which are missing for the current day. One should be able to view in a graph or a list, all students that are missing, present or a combinded dataset of the two options, or a subset of any of those.

## Unhandled Evaluation Resolution View
An unhandled evaluation occurs when a list is tried to be evaluated, i.e. it is checked which signatures are valid to determine which student are present, but the program is unsure if a signature is valid or not it marks the row of the signature on the attendence sheet as an unhandled evaluation.
This view mainly contains a the image of the attendence sheet, where the attendence sheet is straigtend onto the screen and any parts of the image which are not the attendence sheet are removed.
For every marked row a box is drawn around it. The user can interact with the row in such a way that they can select a row and then mark it either as valid or invalid. If row is marked as valid it means that the student is present, otherwise the student is absent.
These changes are all temporary until the user hits a commit button through which those changes are applied. The unhandled evaluation is resolved by this.

## Exporting data
When exporting data from the application there are multiple options to choose the format of the data being exported. The main format for the application is to export the data as an attendence list in an Microsoft Excel file. The attendence list is a single table. It should have the following form:
| Course | Name | 22.11.2023 | 23.11.2023  | 24.11.2023  |
|---|---|---|---|---|
| TIT | M. Mustermann | Present | Present | Absent |
| TIK | M. Musterfrau | Present | Absent | Present |

The date columns show for each name, whether the student was present or absent. There is no reason to differentiate between students that were missing and were excused by the secretariat or students that were missing without reason. In both cases students are marked „absent“. Making this differentiation is beyond the scope of the program.

## Opening the app
The GUI should only open if the user opens it. If the user opens it, it first shows the main page. The only other way to open the app is if the app sends a notification to the user that an unhandled evaluation has happend. When the user interacts with the notification it opens the app with the unhandled evaluation resolution screen. After that the user can close the GUI or continue.
If the user does not open the app via the notification the attendence sheet in question is marked as an unhandled evaluation.

## Configuring the App
All configuration options of the application must be accessible in the GUI itself, there should never be the need to edit a configuration file. Though to provide the possibility to setup the app on different computers with the same configuration, support for a file based configuration should also be added.

## Background task
When the GUI is closed the app itself should continue. In regular intervals it should check wether new attendence sheets have appeared and then process them. If unhandled evaluations occur, send a notification to the user, through which they can open the GUI, as described previously.
The application get its datasheets from the source. This source should be an e-mail mailbox, which is addressed via IMAP. IMAP itself must support both login through a simple username-password combination as well as via XOAuth2. The user should have to enter their login credentials only once, so they need to be stored securly locally. The login credentials should have to be changed later. If the app is uninstalled all traces of the login credentials need to be destroyed.
### Attendance sheet processing
This is the main task done by the background task, therefore it is important that this runs smoothly and does not impact the usability of the PC of the user. This task processes an image of an attendence sheet, determines what signatures are considered valid and which are invalid. The default behaviour for handling invalid signatures is to mark them as unhandled evaluations.
Signature fields should be considered invalid if
-	There is no signature in the field
-	There is more than one signature in the signature field
-	There is no actual signature in the field, there are only a few random lines by people not careless with their pencil
On the other hand signature fields should be considered valid if
-	There signature consists of two names, but the signature is of the form firstname-family name
-	If there are two signatures in the field, but one is crossed out (this is optional to implement)

### Image Processing

- Paper sheet detection
- Reverse perspective transform
- Table detection
- Row/Column detection
- Printed text detection (left column)
- Detection of valid signature fields (only one signature per field, no overlaps, can it qualify as a signature)
- Extraction of list of user and if valid signature is present

Back to main page [here](https://github.com/DHBW-SE-2023/Wiki/blob/main/README.md).