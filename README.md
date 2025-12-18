# FortiCloud SSO Integration with Entra ID

Quick reference for configuring FortiCloud SSO with Microsoft Entra ID.

## Prerequisites

- FortiCloud account with IAM access
- Entra ID tenant with Global/Application Administrator permissions

## Configuration

### Entra ID Setup

1. Azure Portal → Entra ID → Enterprise applications → New application → Create your own application
2. Name it "FortiCloud" and create
3. Single sign-on → SAML
4. Basic SAML Configuration:
   - Identifier: `https://iam.forticloud.com`
   - Reply URL: `https://iam.forticloud.com/saml/acs`
   - Sign on URL: `https://iam.forticloud.com`
5. User attributes & claims:
   - Email: `user.mail` or `user.userprincipalname`
   - First Name: `user.givenname`
   - Last Name: `user.surname`
   - Name ID: `user.userprincipalname` (Email address format)
6. Download Federation Metadata XML
7. Note the Login URL and Azure AD Identifier (Entity ID)
8. Assign users/groups to the application

### FortiCloud Setup

1. FortiCloud → Identity & Access Management → External IdP → Enroll for external IdP
2. Select Microsoft Entra ID
3. Upload the Federation Metadata XML
4. Configure:
   - IdP Entity ID: Azure AD Identifier from above
   - SSO URL: Login URL from above
   - Name ID Format: Email address
5. Save

### Optional: Role Mapping

Map Entra ID groups to FortiCloud permission profiles in External IdP roles.

## Testing

Sign out of FortiCloud, then sign in using the Microsoft SSO option.

## Reference

[Official Documentation](https://docs.fortinet.com/document/forticloud/25.4.a/identity-access-management-iam/113951/configuring-external-idp#EntraID)
