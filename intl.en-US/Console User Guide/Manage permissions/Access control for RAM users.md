# Access control for RAM users {#task_960740 .task}

Resource Access Management \(RAM\) enables you to manage user access to Alibaba Cloud resources. You can reduce risks to your Alibaba Cloud accounts by creating RAM user accounts and managing their permissions.

You can create and manage multiple RAM user accounts with a single Alibaba Cloud account. You can grant different permissions for each RAM user account. This allows each RAM user account to have different access permissions on Alibaba Cloud resources. With RAM, you do not need to share an AccessKey with another account. You can assign minimal permissions to each user to reduce data security risks for your enterprise.

## Create a RAM user account {#section_xsz_mnf_cr1 .section}

1.  Log on to the [RAM console](https://ram.console.aliyun.com/overview) by using an Alibaba Cloud account.
2.  In the left-side navigation pane, choose **Identities** \> **Users**, and click **Create User**.
3.  Configure the required settings.
4.  Select **Console Password Logon** and **Programmatic Access** in the Access Mode field.
5.  Select **Custom Logon Password** in the Console Password field, enter a password, and select **Required at Next Logon** in the Password Reset field.
6.  \(Optional\) Select Required to Enable MFA in the Multi-factor Authentication field and click **OK**.
7.  Save the new account, password, AccessKey ID, and AccessKey Secret. 

    **Note:** We recommend that you save the AccessKey in a timely manner and keep all details strictly confidential.


## Create a user group {#section_rf7_h85_lza .section}

If you attempt to create multiple RAM user accounts, you can group RAM user accounts with identical responsibilities into the same group and authorize the group. This makes it easier to manage users and their permissions.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/overview) by using an Alibaba Cloud account.
2.  In the left-side navigation pane, choose **Identities** \> **Groups**, and click **Create Group**.
3.  Enter the Group Name and Display Name, and click **OK**.

## Grant permissions to a RAM user or group {#section_hp8_s8f_s2z .section}

By default, a new RAM user or group does not have any permissions. You need to grant permissions to the RAM user or group before using the user or group to manage resources by using the console or API operations. The following steps take a RAM user account as an example to grant permissions.

The following NAS policies are provided. You can grant one of the following policies to a RAM user account as required.

-   AliyunNASFullAccess: grants a RAM user account full access to NAS.
-   AliyunNASReadOnlyAccess: grants a RAM user account read-only access to NAS.

**Note:** As only coarse-grained policies are provided in system policies, you can create fine-grained custom policies to meet your business requirements. For more information, see [Create a custom policy](reseller.en-US/Console User Guide/Manage permissions/Create a custom policy.md#).

1.  On the Users page, select a RAM user account to be authorized, and click **Add Permissions**.
2.  In the Add Permissions dialog box, select the required NAS permission and grant the permission to the RAM user account. 

    ![grant permission](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/776283/156576572352606_en-US.png)


