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
