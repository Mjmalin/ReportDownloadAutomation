# ReportDownloadAutomation

This program was made for the Data team at the State of California Department of Education, to download multiple reports from their computer system CALPADS. This saves the Data team time from needing to download each report individually. For confidentiality purposes, some things have been changed or omitted, and as such the full program is not available to the public.

## How it works

This program builds off another program, called calpads. I will refer to the org as "CALPADS" and the program as "the calpads program."

```bash
import calpads
import datetime
import logging

from calpads.client import CALPADSClient
```
After logging the program in to the CALPADS website, the program establishes the lists of reports and schools needed.

```bash
# report and school lists
report_list = ['8.1', '8.1a']
school_list = ['HW', 'MV', 'SL', 'EV', 'WV']
```

Dictionary for school "lea" codes are established, which are what CALPADS uses to find those schools in the system.

```bash
# dictionary for schools and lea codes
lea = {
    'HW' : '012xxxx',
    'MV' : '012xxxx',
    'SL' : '012xxxx',
    'EV' : '014xxxx',
    'WV' : '013xxxx'
}
```
The program then loops through all the reports and schools, preparing all the required fields for the cc.download_report function imported from the calpads program.

```bash
# loops through reports and schools, prepares for download    
for school in school_list:
    for report in report_list:
        #form_inputs for each school and report pairing
        if school == 'HW':
            if report == '8.1':
                form_input = {

            'LEA': 'Citizens of the World Charter School Hollywood',
            'SchoolName': {

                'Citizens of the World Charter School Hollywood-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Hollywood-0000001': True
            }
        }
            elif report == '8.1a':
                form_input = {

            'FromDate': '01/01/2000',
            'ThrouDate': '06/30/2024',
            'SchoolName': {

                'Citizens of the World Charter School Hollywood-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Hollywood-0000001': True
            }
        }

        elif school == "MV":
            if report == '8.1':
                form_input = {

            'SchoolName': {

                'Citizens of the World Charter School Mar Vista-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Mar Vista-0000001': True
            }
        }
            elif report == '8.1a':
                form_input = {

            'FromDate': '01/01/2000',
            'ThrouDate': '06/30/2024',
            'SchoolName': {

                'Citizens of the World Charter School Mar Vista-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Mar Vista-0000001': True
            }
        }

        elif school == 'SL':
            if report == '8.1':
                form_input = {

            'SchoolName': {

                'Citizens of the World Charter School Silver Lake-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Silver Lake-0000001': True
            }
        }
            elif report == '8.1a':
                form_input = {

            'FromDate': '01/01/2000',
            'ThrouDate': '06/30/2024',
            'SchoolName': {

                'Citizens of the World Charter School Silver Lake-012xxxx': True,
                'NPS School Group for Citizens of the World Charter School Silver Lake-0000001': True
            }
        }

        elif school == 'EV':
            if report == '8.1':
                form_input = {

            'SchoolName': {

                'Citizens of the World Charter School East Valley-014xxxx': True,
                'NPS School Group for Citizens of the World Charter School East Valley-0000001': True
            }
        }
            elif report == '8.1a':
                form_input = {

            'FromDate': '01/01/2000',
            'ThrouDate': '06/30/2024',
            'SchoolName': {

                'Citizens of the World Charter School East Valley-014xxxx': True,
                'NPS School Group for Citizens of the World Charter School East Valley-0000001': True
            }
        }

        elif school == 'WV':
            if report == '8.1':
                form_input = {

            'SchoolName': {

                'Citizens of the World Charter School West Valley-013xxxx': True,
                'NPS School Group for Citizens of the World Charter School West Valley-0000001': True
            }
        }
            elif report == '8.1a':
                form_input = {

            'FromDate': '01/01/2000',
            'ThrouDate': '06/30/2024',
            'SchoolName': {

                'Citizens of the World Charter School West Valley-013xxxx': True,
                'NPS School Group for Citizens of the World Charter School West Valley-0000001': True
            }
        }
```

Finally, the cc.download_report function, with all of the required fields. 

```bash
        # downloads all reports
        cc.download_report(

            lea_code=lea[school],
            report_code=report,
            dry_run=False,
            form_data=form_input,
            file_name=f'/Users/cwcstaff/Library/CloudStorage/GoogleDrive-data@cwclosangeles.org/Shared drives/Data & Analytics/Source Docs/Exports and Downloads/CALPADS/For Tableau/{school} - {report}.csv',
            download_format='csv'
```



