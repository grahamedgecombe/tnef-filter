# tnef-filter

## Introduction

`tnef-filter` automatically converts [TNEF][tnef] attachments in an email to
MIME format. It's designed for automated use with a Mail Delivery Agent such as
`procmail` or `maildrop`.

For the benefit of search engines, TNEF attachments are typically named
`winmail.dat`.

## Using with `procmail`

Use a recipe like this in your `.procmailrc` file:

    :0 fw
    * ^X-MS-TNEF-Correlator:
    | /path/to/tnef-filter

As rewriting the emails can break things like DKIM signatures, you might want to
write the original emails to a file for backup purposes:

    :0 cw :
    * ^X-MS-TNEF-Correlator:
    | gzip >> tnef.gz

    :0 afw
    | /path/to/tnef-filter --purge

By default `tnef-filter` will keep the original TNEF attachment, as it doesn't
convert all the information held within it. If you're not worried about data
loss, or have kept a copy of the original email, the `--purge` flag can be used
to override this behaviour and remove the TNEF attachment.

## Dependencies

* [Perl 5][perl]
* [Convert::TNEF][convtnef]
* [File::MMagic][mmagic]
* [MIME::Tools][mimetools]

## License

`tnef-filter` is available under the terms of the [ISC license][isc], which is
similar to the 2-clause BSD license. See the `LICENSE` file for the copyright
information and licensing terms.

[tnef]: https://en.wikipedia.org/wiki/Transport_Neutral_Encapsulation_Format
[perl]: https://www.perl.org/
[convtnef]: https://metacpan.org/pod/Convert::TNEF
[mmagic]: https://metacpan.org/pod/File::MMagic
[mimetools]: https://metacpan.org/pod/MIME::Tools
[isc]: https://www.isc.org/downloads/software-support-policy/isc-license/
