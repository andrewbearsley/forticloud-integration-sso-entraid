# FortiCloud SSO Integration with Entra ID

Configure FortiCloud SSO integration with Microsoft Entra ID (Azure AD).

## Documentation

Full documentation: [Configuring External IdP - Entra ID](https://docs.fortinet.com/document/forticloud/25.4.a/identity-access-management-iam/113951/configuring-external-idp#EntraID)

## Setup Instructions

### Prerequisites

- FortiCloud account with IAM access
- Microsoft Entra ID (Azure AD) tenant
- Global Administrator or Application Administrator permissions in Entra ID

### Step 1: Configure Enterprise Application in Entra ID

1. Sign in to Azure Portal → Microsoft Entra ID
2. Go to **Enterprise applications** → **New application**
3. Select **Create your own application**
4. Name: "FortiCloud" → **Create**
5. Go to **Single sign-on** → **SAML**
6. Configure basic SAML settings:
   - Identifier (Entity ID): `https://iam.forticloud.com`
   - Reply URL (Assertion Consumer Service URL): `https://iam.forticloud.com/saml/acs`
   - Sign on URL: `https://iam.forticloud.com`
7. Save configuration

### Step 2: Configure User Attributes and Claims

1. In SAML configuration, go to **User attributes & claims**
2. Ensure required attributes are mapped:
   - **Email**: `user.mail` or `user.userprincipalname`
   - **First Name**: `user.givenname`
   - **Last Name**: `user.surname`
   - **Name ID**: `user.userprincipalname` (Format: Email address)

### Step 3: Download SAML Metadata

1. In Entra ID SAML configuration, download:
   - **Federation Metadata XML** (save for Step 4)
   - Note the **Login URL** (SAML SSO URL)
   - Note the **Azure AD Identifier** (Entity ID)

### Step 4: Configure FortiCloud External IdP

1. Sign in to FortiCloud → **Identity & Access Management**
2. Go to **External IdP** → **Enroll for external IdP**
3. Select **Microsoft Entra ID**
4. Upload the **Federation Metadata XML** file downloaded from Step 3
5. Configure settings:
   - **IdP Entity ID**: Enter the Azure AD Identifier from Step 3
   - **SSO URL**: Enter the Login URL from Step 3
   - **Name ID Format**: Email address
6. Save configuration

### Step 5: Assign Users in Entra ID

1. In Entra ID Enterprise Application, go to **Users and groups**
2. Click **Add user/group**
3. Select users or groups to grant access to FortiCloud
4. Assign default access role
5. Click **Assign**

### Step 6: Test SSO

1. Sign out of FortiCloud
2. Access FortiCloud login page
3. Select **Sign in with Microsoft** or use the SSO URL
4. Authenticate with Entra ID credentials
5. Verify successful login to FortiCloud

### Step 7: Configure External IdP Roles (Optional)

1. In FortiCloud IAM, go to **External IdP roles**
2. Map Entra ID groups/roles to FortiCloud permission profiles
3. Configure role assignments as needed

## Troubleshooting

- Verify SAML URLs match exactly between Entra ID and FortiCloud
- Check user attribute mappings in Entra ID
- Review FortiCloud audit logs for authentication errors
- Ensure users are assigned to the Enterprise Application in Entra ID

## Reference

- [FortiCloud IAM Documentation](https://docs.fortinet.com/document/forticloud/25.4.a/identity-access-management-iam/113951/configuring-external-idp#EntraID)
