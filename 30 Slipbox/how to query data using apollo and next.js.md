---
created: 2024-06-30 21:05 
modified: Sunday 30th June 2024 21:05:46
alias: 
---
up::  
type:: #note/atomic🌳 
links::
## how to query data using apollo and next.js



[GitHub1s](https://github1s.com/heyxyz/hey/blob/main/apps/web/src/components/Profile/index.tsx
```ts
const {
  data,
  error,
  loading: profileLoading
} = useProfileQuery({
  skip: id ? !id : !handle,
  variables: {
    request: {
      ...(id ? { forProfileId: id } : { forHandle: `${HANDLE_PREFIX}${handle}` })
    }
  }
});

const profile = data?.profile as Profile;

const {
  data: profileDetails,
  isLoading: profileDetailsLoading
} = useQuery({
  enabled: Boolean(profile?.id),
  queryFn: () => getProfileDetails(profile?.id),
  queryKey: ['getProfileDetailsOnProfile', profile?.id]
});

if (!isReady || profileLoading) {
  return (
    <ProfilePageShimmer
      profileList={showFollowing || showFollowers || showMutuals}
    />
  );
}

if (!data?.profile) {
  return <Custom404 />;
}

if (error) {
  return <Custom500 />;
}
```



### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



