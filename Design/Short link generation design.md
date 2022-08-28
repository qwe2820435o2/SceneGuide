# Short link generation design

## 1. Background

The requirements for short links generally have the following characteristics:

* Short links as short as possible

* Need to distinguish short links according to business

* Short links are very short-lived and only need to be used for a short period of time


## 2. Implementation analysis

There are two main difficulties in the whole scheme. 

The first one is the transformation of the correspondence between long and short links, and one-to-one correspondence to ensure uniqueness.

After investigation, the solution that meets this requirement is that generate a globally unique tracking number and the tracking number can be converted into a short code by hexadecimal conversion

The second is the long link deduplication operation when long links generate short links, and the maintenance of the mapping relationship between short links and long links

### 2.1 Globally unique tracking number

Our system has ID generation service which can be used to generate globally unique bill numbers

This ID generation service can generate ids for different businesses and it can support short link generation for our different activities

### 2.2 Base conversion

#### 2.2.1 Generation principle

A short code is usually composed of 62 letters or digits [A-Z, A-Z, 0-9]

The length of a short code can be customized, but generally no more than 8 characters

Here I choose base 10 to base 62. The reason why I choose base 62 is that the characters converted into base 62 are:0123456789 abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz, more in line with our visual habits, and can in the shortest possible short code to support more ID

#### 2.2.2 Business short code

The commonly used short codes are all 6-bit

There are 56.8 billion combinations of 6-bit short codes :(26+26+10)^6 = 56800235584 which meets most application scenarios

To support the short codes of different services, the first short code is set as the service code and the following short code is the service ID code

This has two advantages

One is that a single short link domain name can support a maximum of 62 service short codes

Based on the common 6-bit short code, each service code can reach a maximum of 916132832 which meets our requirements

Such as : https//www.xxx.com/A12tP6

In the traditional short code generation scheme, the ID is shared by all services

Different services are divided into ids based on their ranges

The second advantage of our scheme avoids the traditional scope division problem

Different services can have their own ids, which can be incrementing from 2 bits to ensure the shortest possible short code

For example: https//www.xxx.com/A0

### 2.3 Long link deduplication

There may be repeated long links to generate short links

If there are no special requirements, I will design a one-to-one correspondence here to prevent the waste of short codes

Borrow the setex of redis for deduplication, set the expiration time and do the deduplication measures in the recent period

### 2.4 Short link mapping

The mapping relationship between short links and long links is one-to-one, so here we need to maintain a full mapping relationship and store it in Redis as key-value

## 3. Detail process

