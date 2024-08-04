```
'use client';

import { AnimatePresence, motion, MotionConfig } from 'framer-motion';
import { CheckIcon } from 'lucide-react';
import React, { ButtonHTMLAttributes, useState } from 'react';

const transition = { duration: 0.15 };

type ButtonStatus = 'idle' | 'saving' | 'success';

interface SpinnerButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  onSubmit: () => Promise<void>;
  className?: string;
  children: React.ReactNode;
}

function SpinnerButton({
  children,
  className,
  onSubmit,
  ...rest
}: SpinnerButtonProps) {
  const [status, setStatus] = useState<ButtonStatus>('idle');

  const handleSubmit = async (e: React.MouseEvent<HTMLButtonElement>) => {
    e.preventDefault();
    setStatus('saving');
    await onSubmit();
    setStatus('success');
    setTimeout(() => setStatus('idle'), 2000); // Reset after 2 seconds
  };

  const disabled = status !== 'idle';

  return (
    <MotionConfig transition={{ ...transition, duration: 0.15 }}>
      <button
        type='submit'
        disabled={disabled}
        className={`${className} relative transition duration-200`}
        onClick={handleSubmit}
        {...rest}
      >
        <AnimatePresence mode='wait'>
          {status === 'saving' && (
            <motion.div
              key='a'
              initial={false}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              className='absolute inset-0 flex justify-center py-2'
            >
              <Spinner />
            </motion.div>
          )}

          {status === 'success' && (
            <motion.div
              key='b'
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              className='absolute inset-0 flex justify-center py-2'
            >
              <CheckIcon className='h-full' />
            </motion.div>
          )}
        </AnimatePresence>
        <span className={status === 'idle' ? '' : 'invisible'}>{children}</span>
      </button>
    </MotionConfig>
  );
}

interface SpinnerProps extends React.SVGProps<SVGSVGElement> {
  className?: string;
}

function Spinner({ className, ...rest }: SpinnerProps) {
  return (
    <svg
      viewBox='0 0 24 24'
      className={`${className} h-full w-auto animate-spin`}
      style={{
        animationTimingFunction: 'steps(8, end)',
        animationDuration: '.75s',
      }}
      {...rest}
    >
      <rect
        style={{ opacity: 0.4 }}
        x={11}
        y={2}
        width={2}
        height={6}
        rx={1}
        fill='currentColor'
      />
      <rect
        style={{ opacity: 0.4 }}
        x={18.364}
        y={4.22183}
        width={2}
        height={6}
        rx={1}
        transform='rotate(45 18.364 4.222)'
        fill='currentColor'
      />
      <rect
        x={22}
        y={11}
        width={2}
        style={{ opacity: 0.4 }}
        height={6}
        rx={1}
        transform='rotate(90 22 11)'
        fill='currentColor'
      />
      <rect
        x={19.7782}
        y={18.364}
        width={2}
        style={{ opacity: 0.4 }}
        height={6}
        rx={1}
        transform='rotate(135 19.778 18.364)'
        fill='currentColor'
      />
      <rect
        x={13}
        y={22}
        width={2}
        style={{ opacity: 0.4 }}
        height={6}
        rx={1}
        transform='rotate(-180 13 22)'
        fill='currentColor'
      />
      <rect
        x={5.63603}
        y={19.7782}
        width={2}
        style={{ opacity: 0.6 }}
        height={6}
        rx={1}
        transform='rotate(-135 5.636 19.778)'
        fill='currentColor'
      />
      <rect
        x={2}
        y={13}
        width={2}
        style={{ opacity: 0.8 }}
        height={6}
        rx={1}
        transform='rotate(-90 2 13)'
        fill='currentColor'
      />
      <rect
        x={4.22183}
        y={5.63603}
        width={2}
        height={6}
        rx={1}
        transform='rotate(-45 4.222 5.636)'
        fill='currentColor'
      />
    </svg>
  );
}

export { Spinner, SpinnerButton };

```