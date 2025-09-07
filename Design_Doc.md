# CMCS - Design Document (Part 1: Prototype)

## 1. Assumptions and Constraints

*   *User Roles:* The system will have three distinct user roles:
    1.  *Lecturer (IC):* Can create, edit (until submitted), view, and upload documents for their own claims.
    2.  *Programme Coordinator (PC):* Can view, verify, and approve/reject claims assigned to their programme(s). May have commenting ability.
    3.  *Academic Manager (AM):* Has a global view. Can view and provide final approval/rejection on all claims. This is the final authority.
*   *Non-Functional Prototype:* For Part 1, the application is a static front-end. No data will be saved or processed. Buttons and links will not function.
*   *Technology Stack:* ASP.NET Core MVC (Razor Pages) for the web-based GUI. The database design is conceptual for now (UML), with SQL Server as the intended DBMS.
*   *Supporting Documents:* Lecturers can upload one or more files (e.g., PDF, JPEG, DOCX) per claim to substantiate their hours.

## 2. Database Structure Rationale

The database is designed around the core entity, the Claim. It is central and connects to:
*   *User:* Stores information for all system users (Lecturers, PCs, AMs). A role-based identity system (e.g., ASP.NET Core Identity) will be used later.
*   *ClaimItem:* A claim can have multiple line items (e.g., "Lecture Hours," "Marking," "Meetings"). This allows for flexible calculation based on different hourly rates per task type.
*   *SupportingDocument:* A separate table to handle the one-to-many relationship between a Claim and its uploaded files. Stores the file path, original name, and upload date.
*   *Status:* The status (e.g., Draft, Submitted, UnderReview, ApprovedByPC, ApprovedByAM, Rejected) is tracked for transparency.

This normalized structure avoids data redundancy and allows for efficient querying and future expansion.