---
title: str2num
---

# The `stdlib_str2num` module

[TOC]

## `to_num` - conversion of strings to numbers

### Status

Experimental

### Description

Convert a string or an array of strings to numerical types.

### Syntax

`number = [[stdlib_str2num(module):to_num(interface)]](string, mold)`

### Arguments

`string`: argument has `intent(in)` and is of type `character(*)`.

`mold`: argument has `intent(in)` and is of numerical type. currently: `integer`, `real32` or `real64`.

### Return value

Return a scalar of numerical type (`integer`, `real32` or `real64`).

### Example

```fortran
program example_string_to_number
  use stdlib_kinds, only: dp
  use stdlib_str2num
  implicit none
  character(:), allocatable :: txt
  real(dp) :: x

  txt = ' 8.8541878128e−12 '
  x = to_num( txt , x )
end program example_random_seed
```

## `to_num_p` - conversion of a stream of values in a string to numbers

### Status

Experimental

### Description

Convert a stream of values in a string to an array of values.

### Syntax

`number = [[stdlib_str2num(module):to_num_p(interface)]](string, mold)`

### Arguments

`string`: argument has `intent(in)` and is of type `character(*), pointer`.

`mold`: argument has `intent(in)` and is of numerical type. currently: `integer`, `real32` or `real64`.

### Return value

Return a scalar of numerical type (`integer`, `real32` or `real64`).

### Example

```fortran
program example_str2num
    use stdlib_kinds, only: dp
    use stdlib_str2num
    character(:), allocatable, target :: chain
    character(len=:), pointer :: cptr
    real(dp), allocatable :: r(:)
    integer :: i 

    chain = " 1.234   1.E1 1e0     0.1234E0  12.21e+001 -34.5E1"
    allocate( r(6) )
    cptr => chain
    do i =1, 6
        r(i) = to_num_p( cptr , r(i) ) !> the cptr pointer is shifted within the function
    end do
end program
```