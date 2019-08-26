# Basic cloud disk status table {#EcsApiDiskStatus .reference}

|Code|Description|
|:---|:----------|
|In\_use|In use|
|Available|Available to be attached|
|Attaching|Attaching|
|Detaching|Detaching|
|Creating|Creating|
|Deleting|Deleting|
|Deleted|Deleted|
|ReIniting|Initializing|

The disks in `Deleting` or `Deleted` status cannot be queried using DescribeDisks. These two statuses are internal statuses.

