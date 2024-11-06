# Bulk Deleting Checked-Out Files in SharePoint Online

Recently, I encountered a challenging issue with SharePoint Online involving a bulk file upload gone wrong. Here’s the situation, the problem it caused, and the creative solution a team member suggested to resolve it.

## The Problem

One of our users accidentally uploaded over 300,000 files and folders from their local machine into a SharePoint Online document library. Unfortunately, the library had **Check In/Check Out** enabled, which caused every single file to go into a checked-out state upon upload. Here’s what made it difficult:

1. **Massive Volume of Checked-Out Files**: Since all 300,000+ files were uploaded in bulk, they were all immediately marked as checked out, not by any specific user, but simply stuck in a "checked-out" state.
2. **Deletion Blocked by Check-Out**: The user wanted to delete these files, but because they were all checked out, SharePoint wouldn’t allow direct deletion. I kept seeing the error message: *"It looks like someone has the file open,"* even though no one was actually accessing the files.
3. **List View Threshold Issue**: When I tried to manage these checked-out files by navigating to **Manage Files with No Checked In Version**, SharePoint displayed another error: *"Sorry, something went wrong. The attempted operation is prohibited because it exceeds the list view threshold enforced by the administrator."* This was due to the sheer number of items, which exceeded SharePoint’s list view threshold.

## Attempted Solutions

I tried several approaches to work around the problem:

- **PowerShell Scripting**: I attempted to forcefully delete the folder containing all these files using PowerShell, but I kept getting the same *"file open"* error.
- **ShareGate**: I tried using ShareGate to view and check in the files in bulk. However, ShareGate couldn’t load the files and gave an error about exceeding the list view threshold as well.

## The Solution: Moving Files to a New Library

After trying these approaches, a team member suggested a creative workaround that involved moving the files to a different document library. Here’s how it worked:

1. **Create a New Library**: I created a new document library without the Check In/Check Out feature enabled.
2. **Move the Folder**: I moved the folder containing the 300,000+ files from the original library to the new one. Since this library didn’t have the Check In/Check Out requirement, SharePoint didn’t apply any check-out status to the files during the move.
3. **Delete the New Library**: Once the files were in the new library, I deleted the entire library at once, effectively removing all 300,000+ files in a single operation.

This approach bypassed the check-out status and avoided the list view threshold problem entirely.

## Key Takeaways

- **Beware of Check In/Check Out for Bulk Uploads**: When working with large uploads, it’s best to disable Check In/Check Out if you don’t need it, as it can create issues with bulk check-ins and deletions.
- **List View Threshold**: Always consider the list view threshold limits when working with bulk actions in SharePoint Online. Large libraries can easily exceed this limit and prevent access or changes.
- **Creative Workarounds**: In some cases, moving files to a new library without certain settings (like Check In/Check Out) can provide a workaround for issues that prevent direct deletion.

Thanks to my team member’s suggestion, this solution saved me from hours of manual work, and I hope it can help others facing similar situations in SharePoint Online!

---

Let me know if this version looks good or if there are any further tweaks you’d like!
