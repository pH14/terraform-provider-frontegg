---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "frontegg_workspace Resource - terraform-provider-frontegg"
subcategory: ""
description: |-
  Workspace configuration.
  This is a singleton resource. You must only create one frontegg_workspace resource
  per Frontegg provider.
---

# frontegg_workspace (Resource)

Workspace configuration.

This is a singleton resource. You must only create one frontegg_workspace resource
per Frontegg provider.

## Example Usage

```terraform
resource "frontegg_workspace" "example" {
  name                = "Your Company"
  country             = "US"
  backend_stack       = "Python"
  frontend_stack      = "React"
  open_saas_installed = false

  # If you've configured CNAME record,
  # you can use that custom domain like so:
  # custom_domains = ["frontegg.yourcompany.com"]

  frontegg_domain = "blah.frontegg.com"
  allowed_origins = ["https://yourcompany.com"]

  auth_policy {
    allow_unverified_users           = true
    allow_signups                    = true
    enable_api_tokens                = true
    enable_roles                     = true
    jwt_algorithm                    = "RS256"
    machine_to_machine_auth_strategy = "ClientCredentials"
    jwt_access_token_expiration      = 86400   # 1 day
    jwt_refresh_token_expiration     = 2592000 # 30 days
    same_site_cookie_policy          = "strict"
    auth_strategy                    = "EmailAndPassword"
    allow_tenant_invitations         = true
  }

  mfa_policy {
    allow_remember_device = true
    device_expiration     = 604800 # 7 days
    enforce               = "unless-saml"
  }

  mfa_authentication_app {
    service_name = "Your Company"
  }

  lockout_policy {
    max_attempts = 10
  }

  password_policy {
    allow_passphrases = false
    min_length        = 10
    max_length        = 128
    min_tests         = 2
    min_phrase_length = 6
    history           = 2
  }

  captcha_policy {
    site_key   = "fake-site-key"
    secret_key = "fake-secret-key"
    min_score  = 0.5
  }

  hosted_login {
    allowed_redirect_urls = [
      "http://example.com/a",
      "http://example.com/b",
    ]
  }

  facebook_social_login {
    client_id    = "fake-client-id"
    redirect_url = "fake-redirect-url"
    secret       = "fake-secret"
    customised   = false
  }

  github_social_login {
    client_id    = "fake-client-id"
    redirect_url = "fake-redirect-url"
    secret       = "fake-secret"
    customised   = false
  }

  google_social_login {
    client_id    = "fake-client-id"
    redirect_url = "fake-redirect-url"
    secret       = "fake-secret"
    customised   = false
  }

  microsoft_social_login {
    client_id    = "fake-client-id"
    redirect_url = "fake-redirect-url"
    secret       = "fake-secret"
    customised   = false
  }

  saml {
    acs_url      = "https://mycompany.com/saml"
    sp_entity_id = "my-company"
    redirect_url = "http://localhost:3000"
  }

  oidc {
    redirect_url = "http://localhost:3000"
  }

  reset_password_email {
    from_address  = "me@company.com"
    from_name     = "Your Company"
    subject       = "Reset Your Company Password"
    html_template = "<strong>Reset your password! {{redirectURL}}</strong>"
    redirect_url  = "https://yourcompany.com/reset"
  }

  admin_portal {
    enable_account_settings    = false
    enable_api_tokens          = false
    enable_audit_logs          = false
    enable_personal_api_tokens = false
    enable_privacy             = false
    enable_profile             = false
    enable_roles               = false
    enable_security            = false
    enable_sso                 = false
    enable_subscriptions       = false
    enable_usage               = false
    enable_users               = false
    enable_webhooks            = false

    palette {
      error {
        contrast_text = "#eeeef0"
        dark          = "#ae402c"
        light         = "#FFEEEA"
        main          = "#E1583E"
      }
      info {
        contrast_text = "#eeeef0"
        dark          = "#3c6492"
        light         = "#E2EEF9"
        main          = "#5587C0"
      }
      primary {
        active        = "#278854"
        contrast_text = "#eeeef0"
        dark          = "#36A76A"
        hover         = "#32A265"
        light         = "#A2E1BF"
        main          = "#43BB7A"
      }
      secondary {
        active        = "#E6ECF4"
        contrast_text = "#eeeef0"
        dark          = "#E6ECF4"
        hover         = "#F0F3F8"
        light         = "#FBFBFC"
        main          = "#FBFBFC"
      }
      success {
        contrast_text = "#eeeef0"
        dark          = "#1d7c30"
        light         = "#E1F5E2"
        main          = "#2CA744"
      }
      warning {
        contrast_text = "#eeeef0"
        dark          = "#EAE1C2"
        light         = "#F9F4E2"
        main          = "#A79D7B"
      }
    }
  }
}
```

<!-- schema generated by tfplugindocs -->

## Schema

### Required

- `admin_portal` (Block List, Min: 1, Max: 1) Configures the admin portal. (see [below for nested schema](#nestedblock--admin_portal))
- `allowed_origins` (Set of String) The origins that are allowed to access the workspace.

  This parameter controls the value of the "Origin" header for API responses.

- `auth_policy` (Block List, Min: 1, Max: 1) Configures the general authentication policy. (see [below for nested schema](#nestedblock--auth_policy))
- `backend_stack` (String) The backend stack of the application associated with the workspace.
- `country` (String) The country associated with the workspace.
- `frontegg_domain` (String) The domain at which the Frontegg API is served for this workspace.

  The domain must end with ".frontegg.com" or ".us.frontegg.com".

- `frontend_stack` (String) The frontend stack of the application associated with the worksapce.
- `mfa_policy` (Block List, Min: 1, Max: 1) Configures the multi-factor authentication (MFA) policy. (see [below for nested schema](#nestedblock--mfa_policy))
- `name` (String) The name of the workspace.
- `open_saas_installed` (Boolean) Whether the application associated with the workspace has OpenSaaS installed.
- `password_policy` (Block List, Min: 1, Max: 1) Configures the password policy. (see [below for nested schema](#nestedblock--password_policy))

### Optional

- `bulk_tenants_invites_email` (Block List, Max: 1) Configures the bulk tenants invite email. (see [below for nested schema](#nestedblock--bulk_tenants_invites_email))
- `captcha_policy` (Block List, Max: 1) Configures the CAPTCHA policy in the signup form. (see [below for nested schema](#nestedblock--captcha_policy))
- `custom_domains` (Set of String) List of custom domains at which Frontegg services will be reachable.
  You must configure CNAME for each domain, you can get record values from the portal.
- `facebook_social_login` (Block List, Max: 1) Configures social login with Facebook. (see [below for nested schema](#nestedblock--facebook_social_login))
- `github_social_login` (Block List, Max: 1) Configures social login with GitHub. (see [below for nested schema](#nestedblock--github_social_login))
- `google_social_login` (Block List, Max: 1) Configures social login with Google. (see [below for nested schema](#nestedblock--google_social_login))
- `hosted_login` (Block List, Max: 1) Configures Frontegg-hosted OAuth login. (see [below for nested schema](#nestedblock--hosted_login))
- `lockout_policy` (Block List, Max: 1) Configures the user lockout policy. (see [below for nested schema](#nestedblock--lockout_policy))
- `magic_code_email` (Block List, Max: 1) Configures the one time code email. (see [below for nested schema](#nestedblock--magic_code_email))
- `magic_link_email` (Block List, Max: 1) Configures the magic link email. (see [below for nested schema](#nestedblock--magic_link_email))
- `mfa_authentication_app` (Block List, Max: 1) Configures the multi-factor authentication (MFA) via an authentication app. (see [below for nested schema](#nestedblock--mfa_authentication_app))
- `microsoft_social_login` (Block List, Max: 1) Configures social login with Google. (see [below for nested schema](#nestedblock--microsoft_social_login))
- `new_device_connected_email` (Block List, Max: 1) Configures the new device connected email. (see [below for nested schema](#nestedblock--new_device_connected_email))
- `oidc` (Block List, Max: 1) Configures SSO via OIDC. (see [below for nested schema](#nestedblock--oidc))
- `pwned_password_email` (Block List, Max: 1) Configures the pwned password email. (see [below for nested schema](#nestedblock--pwned_password_email))
- `reset_password_email` (Block List, Max: 1) Configures the password reset email. (see [below for nested schema](#nestedblock--reset_password_email))
- `reset_phone_number_email` (Block List, Max: 1) Configures the reset phone number email. (see [below for nested schema](#nestedblock--reset_phone_number_email))
- `saml` (Block List, Max: 1) Configures SSO via SAML. (see [below for nested schema](#nestedblock--saml))
- `sso_domain_policy` (Block List, Max: 1) Configures how SSO domains are validated. (see [below for nested schema](#nestedblock--sso_domain_policy))
- `sso_multi_tenant_policy` (Block List, Max: 1) Configures how multiple tenants can claim the same SSO domain. (see [below for nested schema](#nestedblock--sso_multi_tenant_policy))
- `user_activation_email` (Block List, Max: 1) Configures the user activation email. (see [below for nested schema](#nestedblock--user_activation_email))
- `user_invitation_email` (Block List, Max: 1) Configures the user invitation email. (see [below for nested schema](#nestedblock--user_invitation_email))
- `user_used_invitation_email` (Block List, Max: 1) Configures the user used invitation email. (see [below for nested schema](#nestedblock--user_used_invitation_email))

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--admin_portal"></a>

### Nested Schema for `admin_portal`

Required:

- `enable_account_settings` (Boolean) Enable access to account settings in the admin portal.
- `enable_api_tokens` (Boolean) Enable access to API tokens in the admin portal.
- `enable_audit_logs` (Boolean) Enable access to audit logs in the admin portal.
- `enable_groups` (Boolean) Enable access to groups in the admin portal.
- `enable_personal_api_tokens` (Boolean) Enable access to personal API tokens in the admin portal.
- `enable_privacy` (Boolean) Enable access to privacy settings in the admin portal.
- `enable_profile` (Boolean) Enable access to profile settings in the admin portal.
- `enable_provisioning` (Boolean) Enable access to provisioning settings in the admin portal.
- `enable_roles` (Boolean) Enable access to roles and permissions in the admin portal.
- `enable_security` (Boolean) Enable access to security settings in the admin portal.
- `enable_sso` (Boolean) Enable access to SSO settings in the admin portal.
- `enable_subscriptions` (Boolean) Enable access to subscription settings in the admin portal.
- `enable_usage` (Boolean) Enable access to usage information in the admin portal.
- `enable_users` (Boolean) Enable access to user management in the admin portal.
- `enable_webhooks` (Boolean) Enable access to webhooks in the admin portal.

Optional:

- `palette` (Block List, Max: 1) Configures the color palette for the admin portal. (see [below for nested schema](#nestedblock--admin_portal--palette))

<a id="nestedblock--admin_portal--palette"></a>

### Nested Schema for `admin_portal.palette`

Optional:

- `error` (Block List) Error color. (see [below for nested schema](#nestedblock--admin_portal--palette--error))
- `info` (Block List) Info color. (see [below for nested schema](#nestedblock--admin_portal--palette--info))
- `primary` (Block List) Primary color. (see [below for nested schema](#nestedblock--admin_portal--palette--primary))
- `secondary` (Block List) Secondary color. (see [below for nested schema](#nestedblock--admin_portal--palette--secondary))
- `success` (Block List) Success color. (see [below for nested schema](#nestedblock--admin_portal--palette--success))
- `warning` (Block List) Warning color. (see [below for nested schema](#nestedblock--admin_portal--palette--warning))

<a id="nestedblock--admin_portal--palette--error"></a>

### Nested Schema for `admin_portal.palette.error`

Required:

- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--admin_portal--palette--info"></a>

### Nested Schema for `admin_portal.palette.info`

Required:

- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--admin_portal--palette--primary"></a>

### Nested Schema for `admin_portal.palette.primary`

Required:

- `active` (String) active color.
- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `hover` (String) hover color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--admin_portal--palette--secondary"></a>

### Nested Schema for `admin_portal.palette.secondary`

Required:

- `active` (String) active color.
- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `hover` (String) hover color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--admin_portal--palette--success"></a>

### Nested Schema for `admin_portal.palette.success`

Required:

- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--admin_portal--palette--warning"></a>

### Nested Schema for `admin_portal.palette.warning`

Required:

- `contrast_text` (String) contrast_text color.
- `dark` (String) dark color.
- `light` (String) light color.
- `main` (String) main color.

<a id="nestedblock--auth_policy"></a>

### Nested Schema for `auth_policy`

Required:

- `allow_signups` (Boolean) Whether users are allowed to sign up.
- `allow_tenant_invitations` (Boolean) Allow tenants to invite new users via an invitation link.
- `allow_unverified_users` (Boolean) Whether unverified users are allowed to log in.
- `auth_strategy` (String) The authentication strategy to use for people logging in.

  Must be one of "EmailAndPassword", "Code", "MagicLink", "NoLocalAuthentication", "SmsCode"

- `enable_api_tokens` (Boolean) Whether users can create API tokens.
- `enable_roles` (Boolean) Whether granular roles and permissions are enabled.
- `jwt_access_token_expiration` (Number) The expiration time for the JWT access tokens issued by Frontegg.
- `jwt_refresh_token_expiration` (Number) The expiration time for the JWT refresh tokens issued by Frontegg.
- `same_site_cookie_policy` (String) The SameSite policy to use for Frontegg cookies.

  Must be one of "none", "lax", or "strict".

Optional:

- `jwt_algorithm` (String) The algorithm Frontegg uses to sign JWT tokens.
- `machine_to_machine_auth_strategy` (String) Type of tokens users will be able to generate.
  Must be one of "ClientCredentials" or "AccessToken".

Read-Only:

- `jwt_public_key` (String) The public key that Frontegg uses to sign JWT tokens.

<a id="nestedblock--mfa_policy"></a>

### Nested Schema for `mfa_policy`

Required:

- `allow_remember_device` (Boolean) Allow users to remember their MFA devices.
- `device_expiration` (Number) The number of seconds that MFA devices can be remembered for, if allow_remember_my_device is true.
- `enforce` (String) Whether to force use of MFA.

  Must be one of "off", "on", or "unless-saml".

<a id="nestedblock--password_policy"></a>

### Nested Schema for `password_policy`

Required:

- `allow_passphrases` (Boolean)
- `history` (Number) The number of historical passwords to prevent users from reusing. Set to zero to disable.
- `max_length` (Number) The maximum length of a password.
- `min_length` (Number) The minimum length of a password.
- `min_phrase_length` (Number)
- `min_tests` (Number) The minimum number of strength tests the password must meet.

<a id="nestedblock--bulk_tenants_invites_email"></a>

### Nested Schema for `bulk_tenants_invites_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--captcha_policy"></a>

### Nested Schema for `captcha_policy`

Required:

- `min_score` (Number) The minimum CAPTCHA score to accept. Set to 0.0 to accept all scores.
- `secret_key` (String) The reCAPTCHA secret key to use.
- `site_key` (String) The reCAPTCHA site key to use.

Optional:

- `ignored_emails` (Set of String) Email addresses that should be exempt from CAPTCHA checks.

<a id="nestedblock--facebook_social_login"></a>

### Nested Schema for `facebook_social_login`

Required:

- `redirect_url` (String) The URL to redirect to after a successful authentication.

Optional:

- `client_id` (String) The client ID of the Facebook application to authenticate with. Required when setting **`customised`** parameter to true.
- `customised` (Boolean) Determine whether the SSO should use customized secret and client ID. When passing true, clientId and secret are also required.
- `secret` (String, Sensitive) The secret associated with the Facebook application. Required when setting **`customised`** parameter to true.

<a id="nestedblock--github_social_login"></a>

### Nested Schema for `github_social_login`

Required:

- `redirect_url` (String) The URL to redirect to after a successful authentication.

Optional:

- `client_id` (String) The client ID of the GitHub application to authenticate with. Required when setting **`customised`** parameter to true.
- `customised` (Boolean) Determine whether the SSO should use customized secret and client ID. When passing true, clientId and secret are also required.
- `secret` (String, Sensitive) The secret associated with the GitHub application. Required when setting **`customised`** parameter to true.

<a id="nestedblock--google_social_login"></a>

### Nested Schema for `google_social_login`

Required:

- `redirect_url` (String) The URL to redirect to after a successful authentication.

Optional:

- `client_id` (String) The client ID of the Google application to authenticate with. Required when setting **`customised`** parameter to true.
- `customised` (Boolean) Determine whether the SSO should use customized secret and client ID. When passing true, clientId and secret are also required.
- `secret` (String, Sensitive) The secret associated with the Google application. Required when setting **`customised`** parameter to true.

<a id="nestedblock--hosted_login"></a>

### Nested Schema for `hosted_login`

Optional:

- `allowed_redirect_urls` (Set of String) Allowed redirect URLs.

<a id="nestedblock--lockout_policy"></a>

### Nested Schema for `lockout_policy`

Required:

- `max_attempts` (Number) The number of failed attempts after which a user will be locked out.

<a id="nestedblock--magic_code_email"></a>

### Nested Schema for `magic_code_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--magic_link_email"></a>

### Nested Schema for `magic_link_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--mfa_authentication_app"></a>

### Nested Schema for `mfa_authentication_app`

Required:

- `service_name` (String) The service name to display in the authentication app.

<a id="nestedblock--microsoft_social_login"></a>

### Nested Schema for `microsoft_social_login`

Required:

- `redirect_url` (String) The URL to redirect to after a successful authentication.

Optional:

- `client_id` (String) The client ID of the Microsoft application to authenticate with. Required when setting **`customised`** parameter to true.
- `customised` (Boolean) Determine whether the SSO should use customized secret and client ID. When passing true, clientId and secret are also required.
- `secret` (String, Sensitive) The secret associated with the Microsoft application. Required when setting **`customised`** parameter to true.

<a id="nestedblock--new_device_connected_email"></a>

### Nested Schema for `new_device_connected_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--oidc"></a>

### Nested Schema for `oidc`

Required:

- `redirect_url` (String) The URL to redirect to after the OIDC exchange.

<a id="nestedblock--pwned_password_email"></a>

### Nested Schema for `pwned_password_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--reset_password_email"></a>

### Nested Schema for `reset_password_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--reset_phone_number_email"></a>

### Nested Schema for `reset_phone_number_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--saml"></a>

### Nested Schema for `saml`

Required:

- `acs_url` (String) The ACS URL for the SAML authentication flow.
- `sp_entity_id` (String) The name of the service provider that will be displayed to users.

Optional:

- `redirect_url` (String) The URL to redirect to after the SAML exchange.


<a id="nestedblock--sso_domain_policy"></a>
### Nested Schema for `sso_domain_policy`

Optional:

- `allow_verified_users_to_add_domains` (Boolean) Whether to allow users to add their own email domain without validating the domain through DNS.
- `bypass_domain_cross_validation` (Boolean) Whether to allow users to sign in even via SSO even if the associated domain has not been validated through DNS.
- `skip_domain_verification` (Boolean) Whether to automatically mark new SSO domains as validated, without validating the domain through DNS.


<a id="nestedblock--sso_multi_tenant_policy"></a>
### Nested Schema for `sso_multi_tenant_policy`

Optional:

- `unspecified_tenant_strategy` (String) Strategy for logging in new users that match SSO configurations for multiple tenants when no tenant has been specified. Either BLOCK or FIRST_CREATED.
- `use_active_tenant` (Boolean) Whether users with existing accounts that match SSO configurations for multiple tenants should be logged in using the SSO for their active (last logged into) account, or whether the unspecified tenant strategy should apply.


<a id="nestedblock--user_activation_email"></a>

<a id="nestedblock--user_activation_email"></a>

### Nested Schema for `user_activation_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--user_invitation_email"></a>

### Nested Schema for `user_invitation_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.

<a id="nestedblock--user_used_invitation_email"></a>

### Nested Schema for `user_used_invitation_email`

Required:

- `from_address` (String) The address to use in the "From" header of the email.
- `from_name` (String) The name to use in the "From" header of the email.
- `html_template` (String) The HTML template to use in the email.
- `subject` (String) The subject of the email.

Optional:

- `redirect_url` (String) The redirect URL to use, if applicable.

  Access this value as "\{\{redirectURL\}\}" in the template.

- `success_redirect_url` (String) The success redirect URL to use, if applicable.
