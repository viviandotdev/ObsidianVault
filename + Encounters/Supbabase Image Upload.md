---
modified: 2025-07-26T18:57:58-04:00
---
1. Create a new bucket
2. Select policies ![[Pasted image 20250726173555.png]]
**USING expression**
```
((bucket_id = 'files'::text) AND (( SELECT (auth.uid())::text AS uid) = (storage.foldername(name))[1]))
```



**Public URL**
```
EXPO_PUBLIC_BUCKET_URL=https://SUPABASE_USERNAME.supabase.co/storage/v1/object/public/files
```
```
EXPO_PUBLIC_BUCKET_URL=https://ttszcmojbdtylwpqxnqt.supabase.co/storage/v1/object/public/files

```