---
created: 2024-07-29 14:21 
modified: Monday 29th July 2024 14:21:12
alias: 
---
p::  
type:: #note/atomic🌳 
links::
## Framer Motion

How does framer motion work?
How does animate presence work?
What are layout animations?

Layout changes
changes that affect neighboring elements
CSS transforms are fast because they do require changing neighboring elements

First, Last, Inverse, Play
Animate layout changes using fast css properties like transform
It inverts any layout changes done by the browser
1. First- measure the position before any layout changes
2. Last- measure position after the layout changes happen
3. Inverse- 
4. Play- 


- **AnimatePresence**- is needed to wrap motion.div in order for exit animations to work
	- **delays** the the **unmounting** of the component until the **exit animation has completed**. lets framer motion know when to apply exit animations or else the component would just be removed instantly. 
- You can add a key to a element for react to know when to mount and unmount it
### Resources
[Inside Framer's Magic Motion](https://www.nan.fyi/magic-motion)

[Animating Radix Primitives with Framer Motion · OlegWock](https://sinja.io/blog/animating-radix-primitives-with-framer-motion)

### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



```
import { AnimatePresence, motion } from 'framer-motion';
import Image from 'next/image';
import { useEffect, useState } from 'react';

interface Movie {
  title: string;
  description: string;
  longDescription: string;
  image: string;
}

export default function SharedLayout() {
  const [activeMovie, setActiveMovie] = useState<Movie | null>(null);

  useEffect(() => {
    function onKeyDown(event: KeyboardEvent) {
      if (event.key === 'Escape') {
        setActiveMovie(null);
      }
    }

    window.addEventListener('keydown', onKeyDown);
    return () => window.removeEventListener('keydown', onKeyDown);
  }, []);
  const width = 68;

  return (
    <>
      <AnimatePresence>
        {activeMovie ? (
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className='absolute inset-0 z-10 bg-black bg-opacity-20'
          />
        ) : null}
      </AnimatePresence>
      <AnimatePresence>
        {activeMovie ? (
          <div className='absolute inset-0 grid place-items-center z-10'>
            <motion.div
              layoutId={`card-${activeMovie.title}`}
              className={`flex h-fit w-[500px] cursor-pointer flex-col items-start gap-4 overflow-hidden p-4 rounded-lg ${'dark:bg-gray-800 dark:text-white bg-white text-black'}`}
            >
              <div className='flex gap-4 w-full'>
                {/* <motion.img
                  layoutId={`image-${activeMovie.title}`}
                  height={56}
                  width={56}
                  alt='Movie'
                  src={activeMovie.image}
                  style={{ borderRadius: 12 }}
                /> */}
                <motion.div layoutId={`image-${activeMovie.title}`}>
                  <Image
                    className=''
                    src={
                      'https://images-na.ssl-images-amazon.com/images/S/compressed.photo.goodreads.com/books/1601937850i/54814676.jpg'
                    }
                    width={width}
                    height={width * 1.5}
                    alt={`books cover`}
                  />
                </motion.div>
                <div className='flex justify-between flex-grow'>
                  <div className='flex flex-col pr-4 p-0'>
                    <motion.h2
                      layoutId={`title-${activeMovie.title}`}
                      className='text-stone-700 text-base font-medium'
                    >
                      {activeMovie.title}
                    </motion.h2>
                    <motion.p
                      layoutId={`description-${activeMovie.title}`}
                      className='text-gray-400 text-xs'
                    >
                      {activeMovie.description}
                    </motion.p>
                  </div>
                  {/* <motion.button
                    layoutId={`button-${activeMovie.title}`}
                    className='rounded-full bg-gray-100 dark:bg-gray-700 px-3 py-1 text-xs font-semibold text-blue-500'
                  >
                    Watch
                  </motion.button> */}
                </div>
              </div>
              <motion.p
                layout
                initial={{ opacity: 0 }}
                animate={{ opacity: 1 }}
                exit={{ opacity: 0, transition: { duration: 0.05 } }}
                className='text-sm text-gray-500 dark:text-gray-400'
              >
                {activeMovie.longDescription}
              </motion.p>
            </motion.div>
          </div>
        ) : null}
      </AnimatePresence>
      <ul className='relative flex w-full flex-col items-center p-0 gap-4  my-12'>
        {MOVIES.map((movie) => (
          <motion.li
            layoutId={`card-${movie.title}`}
            onClick={() => setActiveMovie(movie)}
            key={movie.title}
            className='w-96 p-4 bg-white cursor-pointer rounded-lg border flex flex-col gap-4'
          >
            <div className='flex gap-4'>
              <motion.div
                layoutId={`image-${movie.title}`}
                className='flex-shrink-0'
              >
                <Image
                  className='max-h-[114px] w-full rounded object-cover'
                  src={
                    'https://images-na.ssl-images-amazon.com/images/S/compressed.photo.goodreads.com/books/1601937850i/54814676.jpg'
                  }
                  width={width}
                  height={width * 1.5}
                  alt={`books cover`}
                />
              </motion.div>
              <div className='flex flex-col justify-between flex-grow'>
                <div className='flex flex-col gap-1'>
                  <motion.div
                    layoutId={`title-${movie.title}`}
                    className='text-stone-700 text-base font-medium'
                  >
                    {movie.title}
                  </motion.div>
                  <motion.div
                    layoutId={`description-${movie.title}`}
                    className='text-gray-400 text-xs'
                  >
                    {movie.description}
                  </motion.div>
                </div>
                {/* <div className='flex gap-4'>
                  <div className='flex items-center gap-2'>
                    <div className='w-3.5 h-3.5 bg-zinc-100 rounded-lg flex items-center justify-center'>
                      <div className='w-3.5 h-3.5' />
                    </div>
                    <div className='text-zinc-700 text-xs'>3.9/5</div>
                  </div>
                  <div className='flex items-center gap-2'>
                    <div className='w-3.5 h-3.5 bg-zinc-100 rounded-lg flex items-center justify-center'>
                      <div className='w-3.5 h-3.5' />
                    </div>
                    <div className='text-zinc-700 text-xs'>4/5</div>
                  </div>
                </div> */}
              </div>
            </div>
          </motion.li>
          // <motion.li
          //   layoutId={`card-${movie.title}`}
          //   key={movie.title}
          //   onClick={() => setActiveMovie(movie)}
          //   className='flex w-96 cursor-pointer items-center gap-4 p-0 rounded-lg'
          // >
          //   <motion.img
          //     layoutId={`image-${movie.title}`}
          //     className='h-14 w-14 rounded-xl'
          //     alt='Movie'
          //     src={movie.image}
          //   />
          //   <div className='flex flex-grow items-center justify-between border-b border-gray-200 dark:border-gray-700 last:border-none'>
          //     <div className='flex flex-col py-4'>
          //       <motion.h2
          //         layoutId={`title-${movie.title}`}
          //         className='text-sm font-medium'
          //       >
          //         {movie.title}
          //       </motion.h2>
          //       <motion.p
          //         layoutId={`description-${movie.title}`}
          //         className='text-sm text-gray-500 dark:text-gray-400'
          //       >
          //         {movie.description}
          //       </motion.p>
          //     </div>
          //     <motion.button
          //       layoutId={`button-${movie.title}`}
          //       className='rounded-full bg-gray-100 dark:bg-gray-700 px-3 py-1 text-xs font-semibold text-blue-500'
          //     >
          //       Watch
          //     </motion.button>
          //   </div>
          // </motion.li>
        ))}
      </ul>
    </>
  );
}

const MOVIES = [
  {
    title: 'Interstellar',
    description: 'A journey beyond the stars.',
    longDescription:
      'A team of explorers travel through a wormhole in space in an attempt to ensure humanity’s survival.',
    image: 'https://image.tmdb.org/t/p/w500/rAiYTfKGqDCRIIqo664sY9XZIvQ.jpg',
  },
  {
    title: 'Inception',
    description: 'Your mind is the scene of the crime.',
    longDescription:
      'A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.',
    image: 'https://image.tmdb.org/t/p/w500/qmDpIHrmpJINaRKAfWQfftjCdyi.jpg',
  },
  {
    title: 'The Dark Knight',
    description: 'Why so serious?',
    longDescription:
      'When the menace known as the Joker emerges from his mysterious past, he wreaks havoc and chaos on the people of Gotham.',
    image: 'https://image.tmdb.org/t/p/w500/1hRoyzDtpgMU7Dz4JF22RANzQO7.jpg',
  },
];

```