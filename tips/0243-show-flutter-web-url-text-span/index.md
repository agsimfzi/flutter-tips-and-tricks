# Showing URLs on Flutter web with TextSpan

Did you know?

You can show native-looking URL links on Flutter web using `TextSpan`:

- Create a `Text.rich` or `SelectableText.rich` widget
- Make it look like a web link with a custom text style
- Add a gesture recognizer to open the web link
- Customize the mouse cursor style

![](243.gif)

<!--

// Use Text.rich or SelectableText.rich
Text.rich(
  TextSpan(
    text: uri.toString(),
    // Make it look like a web link
    style: TextStyle(
      color: Theme.of(context).colorScheme.primary,
      decoration: TextDecoration.underline,
      decorationColor: Theme.of(context).colorScheme.primary,
    ),
    // Customize the cursor style
    mouseCursor: SystemMouseCursors.click,
    // Open the web link on tap
    recognizer: TapGestureRecognizer()
      ..onTap = () async {
        await launchUrl(uri, mode: LaunchMode.externalApplication);
      },
  ),
  overflow: TextOverflow.ellipsis,
  maxLines: 3,
)

-->

---

As an alternative, you can wrap the whole thing with a [Link](https://pub.dev/documentation/url_launcher/latest/link/Link-class.html) widget (from the [url_launcher](https://pub.dev/packages/url_launcher) package):

![](243.2.png)

<!--

import 'package:url_launcher/link.dart';

Link(
  uri: uri,
  builder: (BuildContext context, FollowLink? followLink) => Text.rich(
    TextSpan(
      text: uri.toString(),
      // Follow the URL link on tap
      recognizer: TapGestureRecognizer()..onTap = followLink,
      // Customize the cursor style
      mouseCursor: SystemMouseCursors.click,
      // Make it look like a web link
      style: TextStyle(
        color: Theme.of(context).colorScheme.primary,
        decoration: TextDecoration.underline,
        decorationColor: Theme.of(context).colorScheme.primary,
      ),
    ),
    overflow: overflow,
    maxLines: maxLines,
  ),
)

-->

---

Here's a complete `URLTextWidget` that implements the whole thing, in 40 lines of code:

- [URLTextWidget (GitHub Gist)](https://gist.github.com/bizz84/accc69b941a6903cfe4e312f68779ba9)

---

| Previous | Next |
| -------- | ---- |
| [A/B Testing in Flutter](../0242-ab-testing-flutter/index.md) | [TextFormField Setup for Numeric Inputs](../0244-text-form-field-numeric/index.md) |

<!-- TWITTER|https://x.com/biz84/status/1909997182960218589 -->
<!-- LINKEDIN|https://www.linkedin.com/posts/andreabizzotto_did-you-know-you-can-show-native-looking-activity-7315763069161267201-F_73 -->
<!-- BLUESKY|https://bsky.app/profile/codewithandrea.com/post/3lmfdsf5hj22m -->