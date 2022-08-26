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

### 2.3 Long link deduplication

### 2.4 .Short link mapping

## 3. Detail process

