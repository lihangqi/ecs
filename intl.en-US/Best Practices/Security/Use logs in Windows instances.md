# Use logs in Windows instances {#concept_51629_zh .concept}

Logs are records of hardware and software in the system, and system error information. They can also be used to monitor system events. When a server intrusion or system \(application\) error occurs, administrators can quickly locate the problems by using logs and solve the problems quickly, which improves work efficiency and server security substantially. Windows logs can be mainly divided into four categories: system logs, application logs, security logs, and applications and services logs. In this example, we use Windows Server 2008 R2 to introduce the use and analysis of the four categories of logs.

## Open the Event Viewer {#section_m52_fpr_gfb .section}

Follow these steps to open Event Viewer: Open the Run window, type eventvwr, and then click OK to open the Event Viewer.

Then, you can view the following four categories of logs in Event Viewer.

**Note:** You can find the solutions to any error event ID that you can find in these logs in Microsoft knowledge base.

-   **System Logs**

    System logs include events recorded by Windows system components. For example, system logs record failures that occur when loading drivers or other system components during startup.

    The types of events recorded by system components are predetermined by Windows.

-   **Application logs**

    Application logs include events recorded by applications or programs. For example, a database application can record file errors in application logs.

    The types of events recorded are determined by developers.

-   **Security logs**

    Security logs include events such as valid and invalid logon attempts, and resource usage related events such as creation, opening, or deletion of files or other objects.

    Administrators can specify the types of events recorded in security logs. For example, if logon has been set to be audited, logon attempts are recorded in security logs.

-   **Application and service logs**

    Application and service logs are a new type of event logs. These logs store events from a single application or component, rather than events that may affect the global system.


## Modify log path and back up logs {#section_ldp_rwr_gfb .section}

Logs are stored on the system disk by default. The maximum log size is 20 MB by default, and the earliest events are overwritten when 20 MB is exceeded. You can modify the maximum log size according to your needs.

Follow these steps to modify the log path and back up logs:

1.  In the left-side navigation pane of Event Viewer, click **Windows Logs**.
2.  Right click a log name, such as **Application** and click Properties.
3.  In the Log Properties dialog box, you can modify the following settings:
    -   Log path
    -   Maximum log size
    -   Operations executed when maximum event log size is reached

