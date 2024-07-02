three ways to enter the insert mode :

- i for inserting before the current char
- a for appending after the current focuesed char
- o for creating a new line then inserting into it
- shift + i enter insert mode and inser at the start of the line
- shift + a enter the insert mode and appending the end of the line
- shift + o enter insert mode and create new line above

Quite nvim:
:wq write and quite
:q quite if there's no changes
:q! quit and ignore the changes
:set number -activate line number
j down k up h left l right
set relativenumber to activate relative number in vim
set mouse=a activate mouse in nvim
set tabstop=4
set shiftwidth=4
:colorscheme + tab
this is seeting in tem you need a config file vimrc or nvimrc it will be loaded on ever vim nvim lunch

---

u undo changes combines with numbers
ctrl + r redo changes can be compined with numbers
v enters the visual mode
in v mode d when selecting deletes the slected word
in v mod e y for yanking or copying somthing
p for paste after selection /belew P for paste above /before selection dd deletes the whole line
cc delete and enter insert mode change line  
d + shift deletes the rest of the line
c + shift changes the rest of the line
w for next word ,w + shift only space are count a word speration
b for previous word ,b + shift only space are count a word
d+w delete next word
d+b delete previous word
d2w deletes 2 words next  
d2b delete 2 words previous
diw deletes in a word
ciw change in a word
di( delete in ()
di{ delete in {}
e jumpes to the end of the word
0 goes to the start of the line
$ goes to the end of the line
d0 delete to the start of the line
d4 delete to the end of the line
de delte to the end of the word
yiw yank inner word
t* traverse to before next occurence of *
f* find next occurence of *
% jump to the closing of bracket{ or (
d% delete everything including {}
gg start of the file
shift + g to the end of the file
123G gotes to line 123
:123 gotes to line 123
--------all of the above is the fundemtals -------------
[[indent to the right br

]] indent to the left
ctrl + v to visual block mode select column wise
gg + = + G for auto indent a file

---

searching
:/hello search for the next coourence of hello then press n for next n + shift for previous
;?hello search for the previous coourence of hello then press n for previous n + shift for next
select token press # to select the previous occurence \* for the next occurence
ma for making poistions with a them press ' + a (we marked it wit ha ) to return to them '
zz center the current line in the middle of the screen
searching and replaicng and repeating commands
:%s/first/last/g this will search for first and replace it with last through the file
. repeat the last used command
:reg view last stored things copyes cutted and so
deleting cuts the the deleted thing
"7p paste the register number 7
paste the last thing you yanked "0p
------------------macros
qa reocred macro a q quite recording
@a excute macro a
