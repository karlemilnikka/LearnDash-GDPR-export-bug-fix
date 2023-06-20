# Minor LearnDash bug reveals course info

90 days ago, I asked LearnDash to fix a bug that accidentally gives users access to the full list of course names and the number of course steps for each course. If a user who isn’t enrolled in a single course requests a personal data export, the user receives a list of all courses instead of just the user’s enrolled courses. 

This is not an issue for most sites since a full list of courses and course metadata is, by design, publicly available for everyone through the REST API (example[.]com/wp-json/ldlms/v2/sfwd-courses). However, I know that some LearnDash admins prefer not to disclose all courses on their sites and have disabled or restricted LearnDash’s REST API. I’ve therefore published my simple bug fix. 

You can patch the bug on your site by replacing sfwd-lms/includes/class-ld-gdpr.php with my version. I’ll maintain my fork of the class until LearnDash provides an official bug fix. 

Keep in mind! This is not a vulnerability that can be used to access any information that LearnDash isn’t supposed to reveal by design. (But it is a bug because the personal data export shouldn’t disclose the full course list.)

If you don’t want to disclose all courses and their metadata (course description, publish date, modification date, thumbnail, etc.), you must first disable the archive page. You must then either disable LearnDash’s REST API or use a third-party plugin for conditional access, e.g., WP Fusion with Filter Queries enabled. Uncanny Owl’s excellent Not Enrolled Redirect module does not restrict access to the course list or the courses’ metadata through the REST API. 

You can disable LearnDash’s REST API (if you don’t use it) by adding this snippet to your child-theme’s functions.php file. 

```php
add_filter( 'learndash_rest_api_enabled', '__return_false' );
```

## Another bug fix and some additional filters

There are a couple of other modifications to my version of the class. I fixed a bug causing the course status in the personal data export to show the status of the course’s final topic instead of the actual course status. I also added a couple of filters for third-party plugins to use in case my modifications get accepted by the LearnDash developers. 

## Timeline

- 2023-03-19 I reported the bug to LearnDash.
- 2023-03-21 LearnDash replied that they couldn’t confirm if it as a bug but that they would save a note for the developers. 
- 2023-03-19 I sent a copy to LearnDash’s CEO since the support team didn’t take the report seriously. 
- 2023-03-29 LearnDash 4.5.2 was released without the bug fix. I sent a reminder.
- 2023-04-13 LearnDash 4.5.3 was released without the bug fix.
- 2023-05-31 LearnDash 4.6.0 was released without the bug fix. I sent a reminder.
- 2023-06-01 LearnDash’s support replied that they “will inform the developers again and hopefully, we will be able to fix the issue in a future update”.
- 2023-06-01 I told LearnDash that I would have to publish information about the bug before the availability of an official patch if it wasn’t fixed within the 90-day responsible disclosure window.
- 2023-06-13 I submitted my patched version to LearnDash. 
- 2023-06-20 I published this report along with my patched version.
- 2023-06-20 LearnDash’s CEO announced that an official patch will roll out the end of the month. 

