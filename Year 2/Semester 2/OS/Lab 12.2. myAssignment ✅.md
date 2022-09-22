---
tags: [Notebooks/OS]
title: Lab 12.2. myAssignment ✅
created: '2022-05-13T08:30:19.864Z'
modified: '2022-05-22T20:46:51.103Z'
---

# Lab 12.2. myAssignment :white_check_mark:

# Theory
## Section Files 
```
SF_______
|  Body  |
|        |
| Header |
|________|
```
### Header
- special sequences of bytes describing the body

***Restrictions:***
+ Magic = "2BXd"
+ Version $\in$ [13, 93]
+ No_of_sections $\in$ [7, 10]

## Pipes communication protocol
- use named pipes

### String fields :
= | size (1 byte) | contents (-size- nr of bytes) |

- e.g. send error messages or so

:heavy_exclamation_mark: The strings do NOT end with '\0' by default (we need to add \0 if we want to print them or something);

### Number fields :
- unsigned int (sizeof(unsigned int)) = 4 BYTES

### Request message : 

No.|Part of message | description|
|-|-|-|
1.| <req_name> | string-field - 
2.| <nr_param> | number-field
3.| <string_param> | string -field

### Response message

No.|Part of message | description|
|-|-|-|
1.| <req_name> | string-field - 
2.| <response_status> |string-field|
3.| <nr_param> | number-field
4.| <string_param> | string -field

---

# TODO

## 1. Compilation
`gcc -Wall a3.c -o a3 -lrt`

## 2. Pipe-based connection
- our program communicates with the *tester* => 2 * named_pipes:
1. “RESP PIPE 13773” - to be created
2. “REQ PIPE 13773” - to be opened for reading (created by tester)
3. Open for writing RESP pipe 13773
4. Write "CONNECT" to req pipe
5. get "SUCCESS" displayed on our terminal / or display an error message
```
ERROR
cannot create the response pipe | cannot open the request pipe
```

If ***success*** => loop with reading the request message sent by the tester --> handle the request --> send back result

## 3. PING request :white_check_mark:
```
REQUEST : "PING"
RESPONSE : "PING" "PONG" 13773
```
## 4. Create shared mem region :white_check_mark:

```
REQUEST : "CREATE_SHM" 3543026
// that means to create a region of 3543026 bytes of shared mem

RESPONSE: the following behaviour...
// create shared memory region with name "/SZRW41", permissions 664
// use POSIX
// map by program in its own VAS
// send back message:
"CREATE_SHM" "SUCCESS"
"CREATE_SHM" "ERROR"
```

## 5. Write to shared mem request :white_check_mark:

```
REQUEST : "WRITE_TO_SHM" <offset> <value>

RESPONSE: the following behavior
// check if offset is within the shared mem
// check if written bytes are also offsets in the mem region
// send back message:
"WRITE_TO_SHM" "SUCCESS"
"WRITE_TO_SHM" "ERROR"
```

## 6. Memory Map File request :white_check_mark:

```
REQUEST: "MAP_FILE" <file_name>

RESPONSE: the following behavior
//map file with given name in memory
// send back message
"MAP_FILE" "SUCCESS"
"MAP_FILE" "ERROR"
```

## 7. Read from file offset
```
REQUEST: "READ_FROM_FILE_OFFSET" <offset> <no_of_bytes>

RESPONSE: behavior
//read from memory mapped file <no of bytes> bytes from offset <offset>
//write the read bytes to the beginning of the memory region and send back response:

"READ_FROM_FILE_OFFSET" "SUCCESS"
"READ_FROM_FILE_OFFSET" "ERROR"
```

What is success?
- there already exists a shared mem region
- file is mapped in memory
- no_of_bytes + offset < file_size

## 8. Read from file section request

```
REQUEST: "READ_FROM_FILE_SECTION" <section_no> <offset> <no_of_bytes>

RESPONSE: behavior:
//read bytes from an offset in the specified section
//section_no < nr_of_sections
//copy the read bytes back at the beginning of shared memory region
//send back message
"READ_FROM_FILE_OFFSET" "SUCCESS"
"READ_FROM_FILE_OFFSET" "ERROR"
```

## 9. Read from logical memory space offset :heart:

```
REQUEST: "READ_FROM_LOGICAL_SPACE_OFFSET" <logical_offset> <no_of_bytes>
```
### Response:
> read no_of_bytes from the currently memory mapped file starting from an offset calulated in a special way (TBD)

- logical offset = offset in "logical_memory_space" of the file
- logical memory space = contiguous mem area in the memory (that is a mapped SF file)

  - SF sections are loaded in mem starting at an address
  - the header is used only to locate the sections, not loaded in LMS
  - SF section is loaded in LMS to the next available multiple of 2048 bytes after the end of the prv loaded section
  - the order of sections is the one that appears in the header

- what we have to do => be able to find, for a byte in LMS its byte address in the SF.

...
- The read bytes must be copied at the beginning of the shared memory region, before sending
the response message back to the testing program :
```
"READ_FROM_LOGICAL_SPACE_OFFSET" "SUCCESS"
"READ_FROM_LOGICAL_SPACE_OFFSET" "ERROR"
```

## 10. Exit request :white_check_mark:

```
REQUEST: "EXIT"
```
- Close connection / request pipe + remove response_pipe, end loop, terminate

