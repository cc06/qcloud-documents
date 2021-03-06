## Description

Use API to write ACL (Access Control List) for a Bucket. You may either import ACL information by using "x-cos-acl", "x-cos-grant-read", "x-cos-grant-write", "x-cos-grant-full-control" Headers, or import the information via body in XML format. But **you can only choose one method (`Header` or `Body`)**, otherwise an error indicating a conflict will be returned.

Importing new ACL using Put Bucket ACL operation will overwrite existing ACL. Only the owner is allowed to perform the operation.

"x-cos-acl": Enumerated values include public-read, private. "Public-read" means all public users can read the Bucket but only users with private permissions may write to it. "Private" means only users with private permissions may read and write to the Bucket.

"x-cos-grant-read": This means a user who has been granted this permission will be able to read this Bucket

"x-cos-grant-write": This means a user who has been granted this permission will be able to write to this Bucket

"x-cos-grant-full-control": This means a user who has been granted this permission will be able to both read and write to this Bucket


## Request

### Request Syntax


```http
PUT /?acl Http/1.1
Host:<BucketName>-<UID>.<Region>.myqcloud.com
Date: date
Content-Type:application/xml
Content-MD5:MD5
x-cos-acl: [Corresponding permission]
x-cos-grant-read: uin="",uin=""
x-cos-grant-write: uin="",uin=""
x-cos-grant-full-control: uin="",uin=""
Authorization: Auth String
```

### Request Parameter

No particular request parameters

### Request Header

#### Permission-related headers

| Parameter name                     | Description                                       | Type     | Required   |
| ------------------------ | ---------------------------------------- | ------ | ---- |
| x-cos-acl                | Define the ACL attribute of the Bucket. Valid values: private, public-read | String | No    |
| x-cos-grant-read         | Grant read permission to the authorized user. Format: x-cos-grant-read:  uin=" ",uin=" "<Br/> When you need to authorize a sub-account, uin="RootAcountID/SubAccountID"; when you need to authorize the root account, uin="RootAcountID" | String | No    |
| x-cos-grant-write        | Grant write permission to the authorized user. Format: x-cos-grant-write:  uin=" ",uin=" "<Br/> When you need to authorize a sub-account, uin="RootAcountID/SubAccountID"; when you need to authorize the root account, uin="RootAcountID" | String | No    |
| x-cos-grant-full-control | Grant read and write permissions to the authorized user. Format: x-cos-grant-full-control:  uin=" ",uin=" "<Br/> When you need to authorize a sub-account, uin="RootAcountID/SubAccountID"; when you need to authorize the root account, uin="RootAcountID" | String | No    |

### Request Content

| Parameter Name                | Description                                       | Type        |
| ------------------- | ---------------------------------------- | --------- |
| AccessControlPolicy | An independent ACL record                               | Container |
| Owner               | Owner of the identified resource                                  | Container |
| uin                 | User's QQ ID                                    | String    |
| Subacount           | QQ ID of the sub-account                                  | String    |
| AccessControlList   | Information of authorized account and permissions                              | Container |
| Grant               | A single authorization information entry. Each AccessControlList can contain 100 Grant entries  | Container |
| Grantee             | Resource information of authorized user. Type can be RootAcount or SubAccount. For type of  RootAcount, you may enter either a QQ number or "anonymous"(which represents users of all types) for UIN. For type of RootAcount, UIN represents root account, SubAccount represents sub account | Container |
| Permission          | Permission information, enumerated values include READ, WRITE, FULL_CONTROL         | String    |

```XML
<AccessControlPolicy>
  <Owner>
    <uin>ID</uin>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee type="SubAccount">
        <uin>ID</uin>
        <Subaccount> SUBID </Subaccount>
      </Grantee>
      <Permission>Permission</Permission>
    </Grant>
    <Grant>
      <Grantee type="RootAccount">
        <uin>ID</uin>
      </Grantee>
      <Permission>Permission</Permission>
    </Grant>
    <Grant>
      ...
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

## Returned Value

### Response Header

No particular response headers. Please refer to "Common Response Headers" for other returned values

### Response Content

No response content

## Example

### Request

```HTTP
PUT /?acl HTTP/1.1
Host:arlenhuangtestsgnoversion-1251668577.sg.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

<AccessControlPolicy>
  <Owner>
    <uin>2779643970</uin>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee type="RootAccount">
        <uin>2779643970</uin>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### Response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed Jan 18 15:41:31 2017
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```


