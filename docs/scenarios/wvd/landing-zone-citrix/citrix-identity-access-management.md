---
title: Identity and access management for Citrix on Azure
description: Learn how to use Azure role-based access control for identity and access management in your Citrix virtual desktop infrastructure.
author: BenMartinBaur
ms.author: martinek
ms.date: 01/06/2023
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: scenario
ms.custom: think-tank, e2e-avd
---

# Identity and access considerations for Citrix on Azure

This article discusses the various ways of providing identity and access control services for Citrix.

## Design considerations

- Like an Azure subscription, a Citrix Cloud tenant only supports [a single Azure Active Directory (Azure AD) tenant for user or admin authentication](https://docs.citrix.com/en-us/citrix-workspace/secure.html#azure-active-directory). If development and production Azure AD tenant isolation is required for your operational processes, similar isolation should be established for your Citrix Cloud tenants.
- Citrix supports Azure B2B or guest accounts by using SAML authentication in Workspace or Citrix Gateway and Citrix Federated Authentication Service. For more information, see [How to configure Azure AD and SAML for Guest Accounts](https://support.citrix.com/article/CTX312151/how-to-configure-azure-ad-and-saml-tech-preview-for-guest-accounts).
- Citrix includes built-in role-based access control (RBAC) capabilities for core administration and monitoring of the associated Citrix virtual apps and desktops. For more information, see [Delegated administration](https://docs.citrix.com/en-us/citrix-daas/manage-deployment/delegated-administration.html) and [Monitor](https://docs.citrix.com/en-us/citrix-daas/monitor.html).
- The majority of enterprise customers today use full domain services in Azure. They're usually deployed in an [Identity Subscription](/azure/cloud-adoption-framework/ready/enterprise-scale/architecture). You can still use Azure AD as an identity provider for user authentication directly with [Citrix Workspace](https://docs.citrix.com/en-us/citrix-workspace/secure.html#azure-active-directory) in order to use capabilities such as [Azure Multi-Factor Authentication](/azure/active-directory/authentication/concept-mfa-howitworks) and [Conditional Access](/azure/active-directory/conditional-access/overview).
- Single sign-on is supported by using [Citrix Federated Authentication Service](https://docs.citrix.com/en-us/federated-authentication-service/deployment-architectures/azure-ad.html) when using Azure AD or other SAML-based identity providers for authentication.
- Environments that have only Azure AD are possible with support for [Azure AD joined and non-domain joined workloads](https://docs.citrix.com/en-us/citrix-daas/install-configure/azure-joined-ndj-vda-configuration.html).
- The following table summarizes key Citrix functionality for each Azure strategy for hosting domain services. If you're currently in the planning stages of your Azure deployment, review [the comparison of each of these services](/azure/active-directory-domain-services/compare-identity-solutions) with your identity team, and understand their requirements and timelines. Identity is a critical path prerequisite for deployment on Azure.

| Functionality | Azure AD | Azure AD DS | Active Directory Domain Services | No Domain Services |
|:----|:----:|:----:|:----:|:----:|
| Delegated administration in Citrix Cloud | ✓ | ✓ | ✓ | ✓ |
| Machine Creation Services (MCS) | ✓ | ✓ | ✓ | ✓ |
| LDAP/Kerberos | X | ✓ | ✓ | X |
| Group Policy Objects | Use Intune or [Citrix Workspace Environment Management service](https://docs.citrix.com/en-us/workspace-environment-management/service/manage-non-domain-joined-machines.html) | ✓ | ✓ | Use [Citrix Workspace Environment Management service](https://docs.citrix.com/en-us/workspace-environment-management/service/manage-non-domain-joined-machines.html) |
| Authentication to resources | ✓ | ✓ | ✓ | ✓ |
| Domain join | X | ✓ | ✓ | X |
| Citrix Federated Authentication Service | X | X | ✓ | X |

## Design recommendations

Design guidance for [Citrix DaaS on Microsoft Azure is available on Citrix TechZone - Design Guidance for Citrix DaaS on Microsoft Azure](https://docs.citrix.com/en-us/tech-zone/toc/by-solution/daas-for-azure/design-guidance.html). That article highlights the system, workload, user, and network considerations for Citrix technologies in alignment with Cloud Adoption Framework design principles.

## Next steps

Review the critical design considerations and recommendations for resource organization that are specific to the deployment of Citrix on Azure.

- [Resource organization](citrix-resource-organization.md)
