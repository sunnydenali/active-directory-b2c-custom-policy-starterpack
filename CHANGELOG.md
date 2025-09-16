# Changelog

### Set up sign-up and sign-in with a Google account using Azure Active Directory B2C
https://learn.microsoft.com/en-us/azure/active-directory-b2c/identity-provider-google?pivots=b2c-custom-policy
- **Configure Google as an identity provider**
  - ClaimsProvider
  - TechnicalProfile
- **Add a SignInSignUp UserJourney**
  - Add the identity provider to a user journey
    - OrchestrationStep 1 (CombinedSignInAndSignUp)
      - ClaimsProviderSelections element contains a list of identity providers that a user can sign in with.
    - OrchestrationStep 2 (ClaimsExchange)
      - Add a ClaimsExchange element, set the Id to the value of the target claims exchange Id
      - Update the value of TechnicalProfileReferenceId to the Id of the technical profile you created earlier.
**- Configure the relying party policy**
  - Update the ReferenceId to match the user journey ID, in which you added the identity provider.

### Google sign-in error #1

https://accounts.google.com/signin/oauth/error

authError = Cg5pbnZhbGlkX2NsaWVudBIfVGhlIE9BdXRoIGNsaWVudCB3YXMgbm90IGZvdW5kLiCRAw==
client_id = 738729231747-vl1tn95t0hsh6bdum6olqdt3jvb9r99b.apps.googleusercontent.com

flowName  = GeneralOAuthFlow

**Solution**

Where did you see this error message invalid_client — The OAuth client was not found

https://accounts.google.com/signin/oauth/error?authError=Cg5pbnZhbGlkX2NsaWVudBIfVGhlIE9BdXRoIGNsaWVudCB3YXMgbm90IGZvdW5kLiCRAw%3D%3D&client_id=738729231747-vl1tn95t0hsh6bdum6olqdt3jvb9r99b.apps.googleusercontent.com%0A++++++++++++++++++++++++&flowName=GeneralOAuthFlow

?authError=Cg5pbnZhbGlkX2NsaWVudBIfVGhlIE9BdXRoIGNsaWVudCB3YXMgbm90IGZvdW5kLiCRAw%3D%3D

That authError value is a base64-like encoded string.

Here’s the decoded message from that authError parameter:

invalid_client
The OAuth client was not found.

- remove trailing %0A (newline/whitespace) in client_id
- Use <Item Key="client_id">738729231747-vl1tn95t0hsh6bdum6olqdt3jvb9r99b.apps.googleusercontent.com</Item>
- Based on the editor formatting, it might wrap the line, and introduce a newline character at the end of the line.


### Error 400: redirect_uri_mismatch

You can't sign in to this app because it doesn't comply with Google's OAuth 2.0 policy.

If you're the app developer, register the redirect URI in the Google Cloud Console.
Request details: redirect_uri=https://myyorkorg.b2clogin.com/myyorkorg.onmicrosoft.com/oauth2/authresp flowName=GeneralOAuthFlow

https://developers.google.com/identity/protocols/oauth2/web-server#authorization-errors-redirect-uri-mismatch

**Solution**

https://www.url-encode-decode.com/
https://accounts.google.com/signin/oauth/error?authError=ChVyZWRpcmVjdF91cmlfbWlzbWF0Y2gSsAEKWW91IGNhbid0IHNpZ24gaW4gdG8gdGhpcyBhcHAgYmVjYXVzZSBpdCBkb2Vzbid0IGNvbXBseSB3aXRoIEdvb2dsZSdzIE9BdXRoIDIuMCBwb2xpY3kuCgpJZiB5b3UncmUgdGhlIGFwcCBkZXZlbG9wZXIsIHJlZ2lzdGVyIHRoZSByZWRpcmVjdCBVUkkgaW4gdGhlIEdvb2dsZSBDbG91ZCBDb25zb2xlLgogIBptaHR0cHM6Ly9kZXZlbG9wZXJzLmdvb2dsZS5jb20vaWRlbnRpdHkvcHJvdG9jb2xzL29hdXRoMi93ZWItc2VydmVyI2F1dGhvcml6YXRpb24tZXJyb3JzLXJlZGlyZWN0LXVyaS1taXNtYXRjaCCQAypYCgxyZWRpcmVjdF91cmkSSGh0dHBzOi8vbXl5b3Jrb3JnLmIyY2xvZ2luLmNvbS9teXlvcmtvcmcub25taWNyb3NvZnQuY29tL29hdXRoMi9hdXRocmVzcDKkAggBErABCllvdSBjYW4ndCBzaWduIGluIHRvIHRoaXMgYXBwIGJlY2F1c2UgaXQgZG9lc24ndCBjb21wbHkgd2l0aCBHb29nbGUncyBPQXV0aCAyLjAgcG9saWN5LgoKSWYgeW91J3JlIHRoZSBhcHAgZGV2ZWxvcGVyLCByZWdpc3RlciB0aGUgcmVkaXJlY3QgVVJJIGluIHRoZSBHb29nbGUgQ2xvdWQgQ29uc29sZS4KICAabWh0dHBzOi8vZGV2ZWxvcGVycy5nb29nbGUuY29tL2lkZW50aXR5L3Byb3RvY29scy9vYXV0aDIvd2ViLXNlcnZlciNhdXRob3JpemF0aW9uLWVycm9ycy1yZWRpcmVjdC11cmktbWlzbWF0Y2g%3D&client_id=738729231747-vl1tn95t0hsh6bdum6olqdt3jvb9r99b.apps.googleusercontent.com&flowName=GeneralOAuthFlow

https://www.base64decode.net/
https://accounts.google.com/signin/oauth/error?authError=ChVyZWRpcmVjdF91cmlfbWlzbWF0Y2gSsAEKWW91IGNhbid0IHNpZ24gaW4gdG8gdGhpcyBhcHAgYmVjYXVzZSBpdCBkb2Vzbid0IGNvbXBseSB3aXRoIEdvb2dsZSdzIE9BdXRoIDIuMCBwb2xpY3kuCgpJZiB5b3UncmUgdGhlIGFwcCBkZXZlbG9wZXIsIHJlZ2lzdGVyIHRoZSByZWRpcmVjdCBVUkkgaW4gdGhlIEdvb2dsZSBDbG91ZCBDb25zb2xlLgogIBptaHR0cHM6Ly9kZXZlbG9wZXJzLmdvb2dsZS5jb20vaWRlbnRpdHkvcHJvdG9jb2xzL29hdXRoMi93ZWItc2VydmVyI2F1dGhvcml6YXRpb24tZXJyb3JzLXJlZGlyZWN0LXVyaS1taXNtYXRjaCCQAypYCgxyZWRpcmVjdF91cmkSSGh0dHBzOi8vbXl5b3Jrb3JnLmIyY2xvZ2luLmNvbS9teXlvcmtvcmcub25taWNyb3NvZnQuY29tL29hdXRoMi9hdXRocmVzcDKkAggBErABCllvdSBjYW4ndCBzaWduIGluIHRvIHRoaXMgYXBwIGJlY2F1c2UgaXQgZG9lc24ndCBjb21wbHkgd2l0aCBHb29nbGUncyBPQXV0aCAyLjAgcG9saWN5LgoKSWYgeW91J3JlIHRoZSBhcHAgZGV2ZWxvcGVyLCByZWdpc3RlciB0aGUgcmVkaXJlY3QgVVJJIGluIHRoZSBHb29nbGUgQ2xvdWQgQ29uc29sZS4KICAabWh0dHBzOi8vZGV2ZWxvcGVycy5nb29nbGUuY29tL2lkZW50aXR5L3Byb3RvY29scy9vYXV0aDIvd2ViLXNlcnZlciNhdXRob3JpemF0aW9uLWVycm9ycy1yZWRpcmVjdC11cmktbWlzbWF0Y2g=&client_id=738729231747-vl1tn95t0hsh6bdum6olqdt3jvb9r99b.apps.googleusercontent.com&flowName=GeneralOAuthFlow

iq. %y&Ƞ)ںD+
redirect_uri_mismatch
You can't sign in to this app because it doesn't comply with Google's OAuth 2.0 policy.

If you're the app developer, register the redirect URI in the Google Cloud Console.
mhttps://developers.google.com/identity/protocols/oauth2/web-server#authorization-errors-redirect-uri-mismatch *X
redirect_uriH**https://myyorkorg.b2clogin.com/myyorkorg.onmicrosoft.com/oauth2/authresp2**
You can't sign in to this app because it doesn't comply with Google's OAuth 2.0 policy.

If you're the app developer, register the redirect URI in the Google Cloud Console.
mhttps://developers.google.com/identity/protocols/oauth2/web-server#authorization-errors-redirect-uri-mismatch';ݷ׾;uyHlݺnm;}mi
(Wܢ{^(h֦xgz8Yh


**Note:** Update google developer console with redirect URI: https://myyorkorg.b2clogin.com/myyorkorg.onmicrosoft.com/oauth2/authresp


Update TrustFrameworkExtensions.xml file to use the latest Google OAuth endpoints
Authorization endpoint: now uses /o/oauth2/v2/auth
Access token endpoint: now uses https://oauth2.googleapis.com/token
User info endpoint: now uses https://openidconnect.googleapis.com/v1/userinfo

Why update?
The new endpoints support OpenID Connect and are recommended by Google for all new integrations.
The /v2/auth endpoint is required for newer scopes and features.
The new userinfo endpoint is more reliable and future-proof.

