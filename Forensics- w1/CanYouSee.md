CanYouSee

Approach

Extracted ukn_reality.jpg from the provided zip archive and inspected file properties based on the prompt's hint to check image details.

Solution

Read the EXIF tags with exiftool. The Attribution URL tag held the Base64-encoded string YWNhZGVteXtNRTC0RDQ3QV9ISUREM05fYWViZThjMGZ9
exiftool -s3 -AttributionURL ukn_reality.jpg | base64 -d

Flag

academy{ME74D47A_HIDD3N_aebe8c0f}

Takeaway
Always inspect non-standard EXIF fields like Attribution URL or Comment for hidden Base64 strings.
