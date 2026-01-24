---
created: 2025-06-15 13:29
modified: 2025-06-15T13:29:51-04:00
---

type:: #map/content

**Models**
[[Fogg Behavior Model]]
[[Loss Aversion]]


**Books**
[[Hooked by Nir Eyal]]
[[The Courage to be Disliked by Ichiro Kishimi Fumitake Koga]]
[[Subliminal by Leonard Mlodinow]]


[Human Behavioral Biology](https://www.youtube.com/playlist?list=PL-_KSRJxlAgwYUQ08vSWN11Fbwsjv5Gl2)

**Sub topics**
[[Spiral Dynamics]]


```

  <Link
                        href={`/${block.name}`}
                        key={`${block.name}`}
                        className="group flex min-w-0 flex-1 cursor-pointer flex-row items-center gap-3"
                    >
                        <div className="shrink-0 bg-foreground/90 p-[2px] duration-250 transform transition-transform ease-out rotate-[var(--r)] group-hover:rotate-0 rounded-xl" style={{ "--r": "-3.7deg" } as React.CSSProperties}>
                            <div className="size-10 shrink-0 overflow-hidden bg-card rounded-[10px]">
                                <img
                                    src={`https://bytescale.mobbin.com/FW25bBB/image/mobbin.com/prod/content/app_screens/18297ebc-bb03-43ce-b236-49975ad1a2b2.png?f=webp&w=1920&q=85`}
                                    alt={`${block.name} - Free shadcn/ui ${block.name.toLowerCase()} blocks and components`}
                                    className="h-full w-full"
                                />
                            </div>
                        </div>
                        <div className="flex min-w-0 flex-1 flex-col">
                            <p className="truncate text-sm font-medium text-muted-foreground">
                                {block.name} <span className="text-primary">new drop ✨</span>
                            </p>
                            <p className="truncate text-base/tight font-medium text-foreground">
                                {block.description || block.name}
                            </p>
                        </div>
                    </Link>
```


```dataview
LIST
FROM [[#]]
and !outgoing([[#]])

SORT file.link asc
```
