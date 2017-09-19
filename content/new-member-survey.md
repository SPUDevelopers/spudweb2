+++
title = "New Member Survey"
hide_authorbox = true
disable_comments = true
+++

{{< netlify-form name="New Members" >}}
  {{< form-input type="text" label="First Name" id="first-name" placeholder="John" required="true" >}}
  {{< form-input type="text" label="Last Name" id="last-name" placeholder="Smith" required="true" >}}
  {{< form-input type="text" label="Email" id="email" placeholder="smithj5@spu.edu" >}}

  {{< mult-input type="radio" name="is-cs" label="Are you, or will you be, in the Computer Science major at SPU?" required="true" >}}
    {{< form-option label="I am currently enrolled in the CS major." value="In major" >}}
    {{< form-option label="I am intending to enroll in the CS major at a later point." value="Intended" >}}
    {{< form-option label="I do not intend to be part of the CS major." value="Not in CS" >}}
  {{< /mult-input >}}

  {{< mult-input type="radio" name="has-experience" label="Do you have any prior programming experience?" required="true" >}}
    {{< form-option label="Yes" value="true" >}}
    {{< form-option label="No" value="false" >}}
  {{< /mult-input >}}
  {{< form-input type="textarea" id="prev-experience" label="If you answered \"Yes\" above, tell us about your programming experience here." >}}

  {{< mult-input type="select" name="where-heard" label="Where did you hear about SPU Developers (SPUD)?" add_other="true" >}}
    {{< form-option label="Club event" value="event" >}}
    {{< form-option label="Involve-O-Rama" value="Involve-O-Rama" >}}
    {{< form-option label="OrgSync" value="OrgSync" >}}
    {{< form-option label="Poster/Flier" value="poster/flier" >}}
    {{< form-option label="Recommended by a professor" value="Professor recommendation" >}}
    {{< form-option label="Recommended by a friend" value="Friend recommendation" >}}
  {{< /mult-input >}}

  {{< mult-input type="radio" name="contact-email" label="If you entered your email above, can we use it to send you updates about the club?" required="true" >}}
    {{< form-option label="Yes" value="true" >}}
    {{< form-option label="No" value="false" >}}
  {{< /mult-input >}}

{{< /netlify-form >}}
