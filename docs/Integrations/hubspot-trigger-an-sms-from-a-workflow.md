---
title: 'HubSpot: Trigger an SMS from a Workflow'
excerpt: HubSpot enables you to trigger CloudContactAI to send a SMS from a Workflow.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  image: >-
    https://files.readme.io/e210521af43af7d44bd6d9565a281b0b8ff04cc4d14ddfd6646c44b6734a6286-Group_84_1.png
  keywords:
    - sms workflow
    - hubspot
    - trigger
    - sms
  robots: index
next:
  description: ''
---
After you've installed CloudContactAI into you HubSpot account,

1. Login to HubSpot
2. Navigate to Workflows 
3. ![](https://files.readme.io/e42ea85e2ffc5ae5cb47dba450e2c09547ada8b44e3818a6812aea05f6466e66-image.png)

   Click on the "Create workflow" button in the upper right hand corner of the screen
4. Select "From scratch"
5. Select "Contact-based" "Blank workflow"
6. ![](https://files.readme.io/d4766a80f92b782ef0e0567adc86eaef0c85e28ec37c57b61b69e833bec940a1-image.png)

   Click on "Next" in the upper right hand corner.
7. Click on the "Set up triggers" button.
8. ![](https://files.readme.io/5421201cebb0170c2afdd0fa69a768d33210bcf25ca45454ed23eeccfcc95237-image.png)

   Select "When an event occurs"
9. ![](https://files.readme.io/ccae12a6e20c4f1c20b2eb5c57e355ed7626d63ad001c422b4ae3b582cccdb06-image.png)

   On the Add criteria section, pick "Enrolled in workflow"

![](https://files.readme.io/504303d466e89ed28139711e0df2fbac24c1558248bfd02e9f380ec195fc8648-image.png)

10. Hit the "Save" button.
11. Next click on the "+" button.

![](https://files.readme.io/720b364f2a277d7c883310f8ae553442f9df9bc9d7f4237d63807b9492227742-image.png)

12. In the "Browse all actions" section, type CloudContactAI 
13. ![](https://files.readme.io/2cea35b6bd70cbbf0205e2fe6fce6d2d3fb68feb0d9249c32edb2db41ccb6d56-image.png)

    Select "Send SMS Message"
14. Configure your Message, First Name, Last Name, and Phone
15. ![](https://files.readme.io/6978d6f31084474cd17198621e0b5303b646e1b2f3b6ec1745400258ab2d548d-image.png)

    Click on the "Save" button. 
16. Select "Review and publish" in the upper right-hand corner. 
17. On the subsequent dialog, hit "Next"
18. ![](https://files.readme.io/b15915d95e1cce8f11af9727458b226e4b5a97289bb60453e9471217c1ae7182-image.png)

    On the Review workflow dialog, hit "Next". 
19. In the subsequent dialog, Hit "Next" again. 
20. Launch the workflow. 
21. In the upper righthand corner, click on the "Enroll" button
22. ![](https://files.readme.io/e08521a07a5cced2168e71cd483907926f42c2a6c834616b0a8fb5be590834e8-image.png)

    Choose "Individual Contacts"
23. ![](https://files.readme.io/575657a66fa6666c715491ba5bd4ff5f3d36b1d32b65d8507f30af6f0441062a-image.png)

    Select a Contact
24. ![](https://files.readme.io/8e1575120e0e5859ebd0f1725d38c098883c185a9d2293dea435dd5d9821d23c-image.png)
25. Hit the Enroll button
26. Your workflow should trigger, and the SMS should be sent out through CCAI.