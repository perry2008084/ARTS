
## 算法题(Unique Email Addresses)

根据规则查找邮箱地址的数量，规则如下:

1. 邮箱用户名(也就是@符号前的字符串部分)包含`.`则忽略
2. 邮箱用户名中拥有`+`，则忽略后续的字符串

最后对邮箱地址进行统计数量，进行输出.

英文:
```
Every email consists of a local name and a domain name, separated by the @ sign.

For example, in alice@leetcode.com, alice is the local name, and leetcode.com is the domain name.

Besides lowercase letters, these emails may contain '.'s or '+'s.

If you add periods ('.') between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, "alice.z@leetcode.com" and "alicez@leetcode.com" forward to the same email address.  (Note that this rule does not apply for domain names.)

If you add a plus ('+') in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example m.y+name@email.com will be forwarded to my@email.com.  (Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.

Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails? 
```

实例如下:

```
Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails
```

## 解决方案

```javascript
/**
 * @param {string[]} emails
 * @return {number}
 */
var numUniqueEmails = function(emails) {
    var transformed = emails.map((val) => {
        var arr = val.split('@');
        var local = arr[0];
        var index = local.indexOf('+'), newLocal = '';
        if (index != -1) {
            newLocal = local.substring(0, index);
            newLocal = newLocal.replace(/\./gi, '');
        }else {
            newLocal = local;
            newLocal = newLocal.replace(/\./gi, '');
        }
        
        return newLocal + '@' + arr[1];
    });
    
    var filter = Array.from(new Set(transformed));
    
    return filter.length;
};
```