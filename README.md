# Vacation Tracking System (VTS)

## Vision:

A Vacation Tracking System(VTS) will provide individual employees with the capability to manage their own vacation time. sick leave, and personal time off, without having to be an expert in company policy or the local facility's leave policies.

## Functional Requirements:

1. Implements a flexible rules-based system for validating and verifying leave requests.
2. Enables manager approval. (Optional)
3. Provides access to requests for the previous calendar year, and allows requests to be made up to a year and a half in the future.
4. Uses e-mail notification to request manager approval and notify employees of request status changes.
5. Keeps activity logs for all transactions.
6. Enables the HR and system adminstration personnel to override all actions resticted by rules, with the logging of those overrides.
7. Allow managers to directly award personal leave time (with system-set limits).
8. Provides a web service interface for other internal systems to query any given employee's vacation request summary.
9. Interfaces with the HR department legacy systems to retrieve required employee information and changes.

## Non-Functional Requirements:

1. The system should be easy to use
2. Approval for vacation requests process will be faster than manual process.
3. System will reduce time spend by the HR department

## Constraints:

1. Uses existing hardware and middleware.
2. Implemented as an extension to the existing intranet portal system.
3. Must use the portal's single-sign-on mechanisms for all authentication.

## Domain (define problem):

**Human Resource management**: Vacation Time tracking system which enables employees to keep track and manage their vacation days.

## Actors:

**Employee**:
The main user of the system,an Employee uses this system to manager his/her vacation time.<br>
**Manager**:
An employee who has all the abilities and goals of a regular
employee, but with the added responsibility of approving vacation requests
for immediate subordinates. A manager may award subordinates comp
time, subject to certain limits set in the system.<br>
**Clerk**:
A member of the HR department who has sufficient rights to view
employees' personal data and is responsible for ensuring that employees'
information in all HR systems is up to date and correct. An HR clerk can
add or remove nearly any record in the system. In the real world, HR clerks
may or may not be employees; however, if they are employees, they use two
separate login IDs to manage these two different roles.<br>
**System Admin**:
A role responsible for the smooth running of the system's
technical resources (e.g., Web server, database) and for collecting and
archiving all log files.<br>

## Use Cases

### Use case:1

#### **Goal**

The Employee wishes to submit a new request for vacation time.

#### **Preconditions**

The employee is authenticated by the portal framework and
identified as an employee of the company with privileges to manage his or her
own vacation time.

#### **Use case name: Manage Time**

1. The employee begins by selecting a link from the intranet portal to the
   VTS.
2. The VTS uses the employee's credentials to look up the current status
   of all the employee's vacation time requests and outstanding balances.
   Information is displayed for the previous 6 months and up to 18 months
   in the future.
3. The employee wants to create a new request. The employee selects
   one of the categories of vacation time with a positive balance to use.
4. The VTS prompts the employee for the date(s) and time for which to
   request vacation time. The employee should have access to a visual
   calendar to help select and compare chosen dates.
5. The employee selects the desired dates and hours per date (e.g., four
   hours might indicate a half-day vacation time request). The employee
   enters a short title and description (no more than a paragraph in length)
   so that the manager will have more information with which to approve
   this request. When all the information is entered, the employee submits
   the request.
6. If the submitted information is incomplete or incorrect or does not pass
   validation, the Web page is redisplayed, with the errors highlighted and
   documented.
7. The employee has an opportunity to change the information or cancel
   the request.
8. If the information is complete and passes validation, the employee is
   returned to the main VTS home page. If the employee's vacation time
   requests require manager approval, an e-mail is immediately sent to
   the manager(s) authorized to approve the employee's requests.
9. The vacation time request is placed in a state of pending approval.
10. The manager responds to the e-mail by clicking on a link embedded in
    the e-mail or by explicitly logging into the intranet portal and navigating
    to the main VTS home page.
11. The manager may be required to supply necessary authentication credentials
    to gain access to the portal and VTS application.
12. The VTS home page lists the manager's own vacation time requests
    and outstanding balances but also has a separate section listing
    requests pending approval by subordinate employees. The manager
    selects each of these one at a time to individually approve or deny.
13. The VTS displays the details of the requested time and prompts the
    manager to approve or disapprove the request. If the request is disapproved,
    the manager is required to enter an explanation. Once the manager
    submits the result, the internal state of the request is changed to
    approved or rejected.
14. Whether a request is approved or rejected, an e-mail notification is
    immediately sent to the employee who made the request. The manager's
    screen returns to the main VTS home page, and the manager
    may approve other outstanding requests, make a request for him- or
    herself, or simply leave the VTS application.

#### **Flowchart**

<br>
<br>

<div style="text-align:center">
<img src="use-case-01\Employee-Manager-flowchart-diagram.png" />
</div>

<br>

#### **Sequence Diagram**

<br>
<br>

<div style="text-align: center">
<img src="use-case-01\Employee-Manager-sequence-diagram.png">
</div>

<br>
<br>

#### **Pseudocode:**

```
createVacationRequest(int employeeId, String vacationType, Date startDate, Date endDate)
   if getRemainingBalance(employeeId, vacationType) < (endDate - startDate)
      showError
      Redirect to Requests homepage
   else
      sendRequest(employeeId, vacationType, startDate, endDate)
      if isRequireManagerApproval(employeeId)
         sendRequestManagerApprovalEmail(employee, vacationType, startDate, endDate)
```

<hr>

### Use case:2

#### **Goal**

The employee wants to withdraw an outstanding request for vacation time.

#### **Preconditions**

An employee has made a vacation time request, and that
request has yet to be approved or denied by an authorized manager. See also
main flow preconditions.

#### **Use case name: Withdraw Request**

1. The employee navigates to the VTS home page through the intranet
   portal application, which identifies and authenticates the employee with
   the privileges necessary for using the VTS.
2. The VTS home page contains a summary of vacation time requests,
   outstanding balances per category of time, and the current status of all
   active vacation time requests for the previous 6 months and up to 18
   months in the future.
3. The employee selects a vacation time request to withdraw, one that is
   currently pending approval.
4. The VTS prompts the employee to confirm the request to withdraw the
   previously submitted vacation time request.
5. The employee confirms the desire to withdraw, and the request is
   removed from the manager’s list of pending approvals.
6. The system sends a notification e-mail to the manager.
7. The system updates the request state to withdrawn.

#### **Flowchart**

<br>
<br>

<div style="text-align:center">
<img src="use-case-02\Employee-withdraw-pending-request-flowchart.png" />
</div>

<br>

#### **Sequence Diagram**

<br>
<br>

<div style="text-align: center">
<img src="use-case-02\Employee-withdraw-request-sequence-diagram.png">
</div>

<br>
<br>

#### **Pseudocode:**

```
pendingRequestWithdraw(int employeeId, int requestId)
   updateRequestStatusToWithdraw(employeeId, requestId)
   Integer managerId = hasManager(employeeId)
   if(managerId != null)
      sendToEmailServiceToNotifiyManager(employeeId, managerId)
```

<hr>

### Use case:3

#### **Goal**

The employee wants to cancel an approved vacation time request.

#### **Preconditions**

The employee has a vacation time request that has been
approved and is scheduled for some time in the future or the recent past (previous
5 business days). See also main flow preconditions.

#### **Use case name: Cancel Approved Request**

1. The employee navigates to the VTS home page through the intranet
   portal application, which identifies and authenticates the employee with
   the privileges necessary for using the VTS.
2. The VTS home page contains a summary of vacation time requests,
   outstanding balance per category of time, and the current status of all
   active vacation time requests for the previous 6 months and up to 18
   months in the future.
3. The employee selects a vacation time request to cancel, one that is in
   the future (or recent past) and has been approved.
4. If the request is in the future, the employee is prompted to confirm the
   cancellation. If the request is in the recent past, the employee is
   prompted to confirm the cancellation and provide a short explanation. If
   the employee approves the cancellation and provides the required information,
   an e-mail notification is sent to the manager, and the state of
   the request is changed to canceled. The time allowances used to make
   the request are returned to the employee. The employee can also abort
   the cancellation, effecting no changes to the current requests.
5. The employee is returned to the main VTS home page. The summaries
   are updated to reflect any

#### **Flowchart**

<br>
<br>

<div style="text-align:center">
<img src="use-case-03\Employee-cancel-approved-request-flowchart.png" />
</div>

<br>

#### **Sequence Diagram**

<br>
<br>

<div style="text-align: center">
<img src="use-case-03\Employee-cancel-approved-req-sequence-diagram.png">
</div>

<br>
<br>

#### **Pseudocode:**

```
cancelApprovedRequest(int requestId, int employeeId)
   if(requestInFuture(requestId))
      askUserConfirmation()
   else
      askUserConfirmationAndExplanation()

   if(IsUserAbortCancelProcess())
      return

   updateRequestStatus(requestId, employeeId)
   updateEmployeeOutStandingBalance(employeeId)

   Integer managerId = getEmployeeManager(employeeId)
   if(managerId != null)
      sendEmailToManagerUsingEmailService(employeeId, managerId)

```
