# ISA, GS, ST (The X12 Envelopes)

**30-Second Explanation**: The nested envelopes that wrap every single X12 file, exactly like a letter inside a folder inside a shipping box.

**2-Minute Explanation**: Every X12 file has a strict 3-tier envelope structure:
1. **ISA/IEA (Interchange)**: The shipping box. It identifies the Sender and Receiver IDs (who is shipping the box and who is getting it).
2. **GS/GE (Functional Group)**: The folders inside the box. It groups similar transactions together (e.g., all 837 claims go in one folder, all 270s in another).
3. **ST/SE (Transaction Set)**: The actual letter. This is where the specific claim or inquiry data lives.

**Purpose**: Routing, batching, and parsing control.

**Who sends it**: Every EDI system.

**Who receives it**: Every EDI system.

**Input**: Configuration data for trading partners.

**Output**: The outer wrappers of an X12 string.

**Common Errors**: 
- ISA control numbers not matching the IEA control number.
- Incorrect Sender/Receiver IDs, causing the Edifecs gateway to instantly reject the file with a TA1.

**Real Project Example**: When setting up the Route for Humana, the inbound 276 payload was identified and routed specifically by inspecting the ISA Sender ID and the GS Functional ID.

**Interview Questions**:
- *Explain the envelope structure of an X12 file.* (Answer: ISA is the Interchange envelope for routing. GS is the Functional Group envelope for batching similar types. ST is the Transaction Set envelope containing the actual data).
