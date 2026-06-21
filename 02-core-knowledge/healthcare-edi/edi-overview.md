# Healthcare EDI Overview

**30-Second Explanation**: EDI (Electronic Data Interchange) is the digital language of healthcare. It is how hospitals, pharmacies, and insurance companies talk to each other without using paper, faxes, or humans.

**2-Minute Explanation**: Before EDI, a hospital had to print a paper bill and mail it to an insurance company, where a data entry clerk manually typed it into a computer. EDI standardizes this data into strict, machine-readable formats (mostly X12 in the US). By forcing every payer and provider to use the exact same format for a claim (837) or a payment (835), the entire US healthcare system can be automated. It is heavily regulated by HIPAA to ensure security and consistency.

**Purpose**: To completely automate the exchange of massive volumes of healthcare administrative and financial data.

**Who sends it**: Providers, Payers, Clearinghouses, Employers.

**Who receives it**: Providers, Payers, Clearinghouses.

**Input**: Clinical encounters, patient registrations, payments.

**Output**: Standardized X12 or JSON/XML payloads.

**Common Errors**: 
- Failing SNIP validations (structural or syntax errors).
- Passing unencrypted PHI in plain text.

**Real Project Example**: At Humana, I modernized the EDI pipeline for 276/277 transactions. Instead of relying on legacy batch EDI processing, we exposed real-time APIs that ingested EDI, parsed it via Edifecs, and returned an EDI response in under 3 seconds.

**Interview Questions**:
- *Why is EDI still used instead of standard JSON APIs everywhere?* (Answer: Because changing a multi-trillion dollar industry takes decades, and X12 EDI is highly compressed and heavily regulated by HIPAA law).
