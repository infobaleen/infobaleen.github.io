# Exports

## Voyado
In Voyado, you have the opportunity to use your segments from Sift Lab for emails, marketing automation, SMS marketing, and social pushing towards Instagram, Facebook, and Google. 
You can easily export segments to Voyado from Sift Lab, where they are made available in two different ways depending on the use case.

These are
* __Customer attributes__: Used for dynamic segmentations, those saved as `Scheduled: Automatic`, that are updated periodically, for example daily or weekly. Values are set on predefined attributes in Voyado with names like 'Sift Lab: Dynamic Segment 1', 'Sift Lab Dynamic Segment 2', etc., depending on the segmentation.
* __Labels__: Used for one-time segmentations, such as for one-off campaigns.

To export segments to Voyado, filters are required on users to ensure they exist in Voyado, are not deleted, and have a contact type that supports labels or attributes.

An exported segmentation usually becomes visible in Voyado within five to ten minutes depending on size. If this does not happen, please refer to the Troubleshooting section for more information.

### Filters
To export segments to Voyado, a filter on users is required based on the targeted channel:
* `Status email in (Active)` or `Status sms in (Active)`

This ensures that the user is not deleted, has consent, and can receive communication in the chosen channel.

Depending on your Voyado environment, you may also need a user filter on contact type to export segments, both for one-time segmentations and dynamic segmentations. Typically, a segmentation is filtered on contact types `member` and `contact`:
* `Contact type in (member, contact)`

You will receive information about the required filters for your setup from you customer success manager.

It is also common to add filters on country depending on your business model.

Here is an example of user fliters applied to a segmentation.
![Screenshot 2024-05-28 at 10 25 13](https://github.com/infobaleen/customer-success/assets/8920436/bb61e3b3-27e2-4080-9496-85fd3506bd15)

### Labels (etiketter)
When a segmentation is exported as labels in Voyado, they are available under Segmentation / Labels and can be filtered in Voyado's segmentation tool under 'Labels'.

![Screenshot 2024-05-23 at 10 03 00](https://github.com/infobaleen/customer-success/assets/8920436/8f900103-6ea4-4098-bde2-dea61ea1bc8c)

![Screenshot 2024-05-23 at 10 05 14](https://github.com/infobaleen/customer-success/assets/8920436/9a26e674-0d3e-4407-9d61-9d9334d17307)

The name of the label consists of the name of the segment in Sift Lab and a unique ID. Every time a segmentation is exported, a new label is created, and old labels are not changed.

Please note that when a segment is exported as a label to Voyado, it has no connection to the segment in Sift Lab. Updates in Sift Lab do not affect the segment in Voyado, and vice versa.

### Customer attributes
Dynamic segmentations, which are segments saved as 'Scheduled: Automatic' and updates regularly, are exported as attributes on customers in Voyado. The attributes are string fields where the value is set to the name of the segmentation in Sift Lab. There are ten attributes available by default: 'Sift Lab: Dynamic Segment 1', 'Sift Lab: Dynamic Segment 2', etc. More can be added as needed.

Selecting a destination in Sift Lab means selecting the attribute for export and is made in the settings for the segmentation. Only one segmentation can use a specific attribute. Therefore, only the attributes that are not used by anyone else are selectable.

![Screenshot 2024-05-28 at 08 07 11](https://github.com/infobaleen/customer-success/assets/8920436/f2038845-211d-4626-a004-85eb87554092)

The attributes can be filtered in the segmentation tool in Voyado and can be easily found by searching for, for example, 'sift'.

![Screenshot 2024-05-28 at 07 56 27](https://github.com/infobaleen/customer-success/assets/8920436/b5bad9bf-c91c-47e6-8c25-9d860023c420)

By setting a condition that the value of the field should be the same as the name of the segmentation, users belonging to the segment are filtered out.

![Screenshot 2024-05-28 at 08 13 24](https://github.com/infobaleen/customer-success/assets/8920436/ee7fcc46-14ce-4f2d-911a-ac531dcd8db6)

### Troubleshooting
If an exported segmentation does not appear in Voyado within 30 minutes, check Voyado's integration log and filter by type 'MemberImport'. You can find the log under Administration / Integration Log.

![Screenshot 2024-05-20 at 09 48 12](https://github.com/infobaleen/customer-success/assets/8920436/ee45b28c-02ef-4bb3-9e03-392d28528c85)

Click on a row to see more details about what caused the failed import.

![Screenshot 2024-05-20 at 09 49 29](https://github.com/infobaleen/customer-success/assets/8920436/43000255-f6f7-45ae-abf2-8be4e1821ee9)

Contact support@siftlab.com and attach any error messages from the integration log related to exports from Sift Lab.
