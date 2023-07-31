## Summary:
Given a keyboard with its actual keycaps swapped, determine the keys needed to be pressed in order to get the desired output

# INTUITION:
- Consider a imagery keyboard in which the *switches* are numbered from 0 to 25. Here initially the mapping of *switches* to *key-caps* are **0->A, 1->B, etc..**. Since the keycaps are swapped, not the switches itself, we will require 2 dictionary(unordered map) to track which switch does the current key-caps reside in and the key-caps position.
- consider swapping **A->B, B->C**, then for outputting **A**, we need to press **C**, for **B** we need **A**, for **C** we need **B**(explains why single map won't work).

# IMPLEMENTATION:
```python
  
def solve():  
    # given the order of swaps of key-caps in keyboard, output the map for the given string  
    switches = {int(i): chr(k) for i, k in enumerate(range(ord('A'), ord('Z') + 1))}  
    caps_pos = {chr(k): int(i) for i, k in enumerate(range(ord('A'), ord('Z') + 1))}  
    swaps = int(inp())  
    for _ in range(swaps):  
        a, b = inp().split()  
        curr_pos_a, curr_pos_b = caps_pos[a], caps_pos[b]  
        switches[curr_pos_a], switches[curr_pos_b] = b, a  
        caps_pos[a], caps_pos[b] = curr_pos_b, curr_pos_a  
  
    s = inp().strip()  
    new_s = str()  
    for i in s:  
        curr_pos = ord((i.lower())) - ord('a')  
        curr_letter = switches[curr_pos]  
        if 'a' <= i <= 'z':  
            new_s += curr_letter.lower()  
        else:  
            new_s += curr_letter  
  
    print(new_s)  
'''  
test case 1:  
1 H W  
Helloworld  
ans : Wellohorld  
test case 2:  
2 A B  
B C  
AbcD  
ans : CabD  
test case 3:  
10  
Y A  
M K  
G L  
V X  
O Z  
L V  
X N  
L L  
J D  
V N  
gVXLpVAZNP  
ans :nVLGpVYOXP  
'''
```