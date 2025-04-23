---
modified: 2025-04-23T06:40:28-04:00
---
```
6
7
8
1
3
5
6
7
8
1
2.
3
4
5
interface InputProps {
post: Post;
updatePost: (id: string, updates: { key: string, value: string }[]) => void;
textArray: string!;
setContentHeight: (height: number)  =>  void;
}
export const renderText = ({ textArray, post }: { textArray: string[l, post?: Post }) => {
if (ItextArray) return null;
return <Text>
{textArray?.map((part, index)
= {
if (part?.startsWith('#') || part?.startsWith('®")) €
const
tag = part?. toUpperCase()
return
‹Text key=(index)
size="md"
className=" font-bold"
```