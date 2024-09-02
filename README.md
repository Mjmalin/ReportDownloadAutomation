# ReportDownloadAutomation

This program was made for the Data team at CALPADS, the computer system of the State of California Department of Education, to download multiple reports at once. For confidentiality purposes, some things have been changed or omitted, and as such the full program is not available to the public.

## How it works

This program builds off another program, CALPADS.

```bash
import calpads
import datetime
import logging

from calpads.client import CALPADSClient
```


