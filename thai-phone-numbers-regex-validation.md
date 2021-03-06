
# PHONE NUMBERS IN THAILAND AND THEIR REGEX VALIDATION
* BASED ON https://en.wikipedia.org/wiki/Telephone_numbers_in_Thailand
* AUTHOR: https://github.com/underlines/
* VERSION: 20200701-3

## COMPLETE REGEX FOR ALL GROUPS:
```
^02\d{6,7}$|^(03[2-9]|04[0-9]|05[0-6])\d{6}$|^07[3-7]\d{6}$|^0[6-9]\d\d{7}$
```
# How to create the Regular Expression
The above regex is compromised from the following parts, and simply combined with an OR pipe `|`
## LANDLINE, BANGKOK GROUP
* SPECIFICATION: 02 + (6-7 digits)
* REGEX: `^02\d{6,7}$`
### TEST
#### MATCH
```
02123456
021234567
```

#### NO MATCH
```
(wrong area code)
03123456
(too long)
0212345678
(too short)
0212345
```

## LANDLINE, PROVINCES GROUP I
* SPECIFICATION: 032-056 + (6 digits)
* REGEX: `^(03[2-9]|04\d|05[0-6])\d{6}$`

### TEST 
#### MATCH
```
032123456
056123456
```

#### NO MATCH
```
031123456 (wrong area code)
03212345 (too short)
0321234567 (too long)
```

## LANDLINE, PROVINCES GROUP II
* SPECIFICATION: 073-077 + (6 digits) Province Landline
* REGEX: `^07[3-7]\d{6}$`

### TEST
#### MATCH
```
073123456
077123456
```

#### NO MATCH
```
072123456 (wrong area code)
07312345 (too short)
0731234567 (too long)
```


## MOBILE GROUP
* SPECIFICATION: 060-099 + (7 digits)
* REGEX: `^0[6-9]\d\d{7}$`

### TEST
#### MATCH
```
0601234567
0991234567
```

#### NO MATCH
```
0591234567 (wrong area code)
1001234567 (wrong area code)
099123456 (too short)
09912345678 (too long)
```

