# Hellokitty-keshav
Hello kittu surprise for kismis
// HelloKittyForKeshav.jsx
// Single-file React component (Next.js page compatible)
// Tailwind CSS assumed. Uses Framer Motion for animations.
// How to use:
// 1) Create a Next.js app (`npx create-next-app@latest`) and enable Tailwind.
// 2) Save this file as `app/hellokitty/page.jsx` (Next 13 app dir) or `pages/hellokitty.jsx`.
// 3) Install dependencies: `npm i framer-motion`
// 4) Replace the placeholder images and text where noted.
// 5) Deploy to Vercel (connect your GitHub repo, push branch) — Vercel will give you a URL like `yourname.vercel.app`.
// 6) Generate a QR code from that URL (many free sites exist) and send it to Keshav.

import React, {useState} from 'react'
import {motion} from 'framer-motion'

export default function HelloKittySurprise(){
  const [opened, setOpened] = useState(false)
  const [showGallery, setShowGallery] = useState(false)

  // PERSONALIZE THESE
  const recipientName = 'Keshav' // change to Keshav
  const senderName = 'Priyanshi' // change if you want
  const heroMessage = `Hi ${recipientName} 💕 I made this for you — open the surprise!`
  const letterLines = [
    "Tumhara smile mera favourite hai.",
    "Har choti baat mein tumhein yaad karti hoon.",
    "Bas itna hi: I miss you — ${senderName} "
  ]

  // Replace these image URLs with your photos or hosted assets
  const gallery = [
    '/images/sample1.jpg',
    '/images/sample2.jpg',
    '/images/sample3.jpg'
  ]

  return (
    <div className="min-h-screen bg-pink-50 flex items-center justify-center p-6">
      <div className="max-w-2xl w-full bg-white/80 backdrop-blur-md rounded-2xl shadow-2xl p-6 border border-pink-200">

        {/* Header */}
        <div className="flex items-center gap-4">
          <img src="/images/hellokitty-icon.png" alt="Hello Kitty" className="w-16 h-16" />
          <div>
            <h1 className="text-2xl font-extrabold text-pink-600">Hello Kitty Surprise</h1>
            <p className="text-sm text-pink-500">A tiny surprise created with ❤️</p>
          </div>
        </div>

        {/* Card */}
        <div className="mt-6">
          {!opened ? (
            <motion.button
              whileTap={{scale:0.98}}
              whileHover={{scale:1.02}}
              onClick={()=>setOpened(true)}
              className="w-full bg-pink-500 text-white py-4 rounded-xl shadow-inner font-bold text-lg"
            >
              Open the surprise for {recipientName}
            </motion.button>
          ) : (
            <motion.div
              initial={{opacity:0, y:20}}
              animate={{opacity:1, y:0}}
              transition={{duration:0.45}}
              className="mt-4"
            >
              <div className="rounded-lg p-4 bg-gradient-to-br from-pink-50 to-white border border-pink-100">
                <p className="text-pink-700 text-lg font-semibold">{heroMessage}</p>

                {/* Little animated sticker */}
                <motion.div
                  animate={{rotate:[-6,6,-6]}}
                  transition={{repeat: Infinity, duration:2, ease: 'easeInOut'}}
                  className="mt-4 flex items-center gap-3"
                >
                  <img src="/images/kitty-sticker.png" alt="kitty" className="w-20 h-20" />
                  <div>
                    <p className="text-sm text-pink-600">Tap the icons to see more</p>
                    <div className="flex gap-2 mt-2">
                      <button onClick={()=>setShowGallery(!showGallery)} className="px-3 py-1 rounded-full bg-pink-100 text-pink-700 text-sm">Photos</button>
                      <button onClick={()=>document.getElementById('letter')?.scrollIntoView({behavior:'smooth'})} className="px-3 py-1 rounded-full bg-white border border-pink-200 text-pink-600 text-sm">Letter</button>
                    </div>
                  </div>
                </motion.div>

                {/* Gallery */}
                {showGallery && (
                  <div className="mt-4 grid grid-cols-2 gap-3">
                    {gallery.map((g,i)=> (
                      <img key={i} src={g} alt={`photo-${i}`} className="rounded-lg object-cover w-full h-36 shadow-md" />
                    ))}
                  </div>
                )}

                {/* Mini interactive quiz */}
                <div className="mt-4 p-3 bg-white rounded-lg border border-pink-50">
                  <p className="text-sm text-pink-600 font-medium">Mini quiz — just for fun 🎀</p>
                  <small className="block text-xs text-pink-400">(Click an answer)</small>
                  <div className="mt-2 grid grid-cols-2 gap-2">
                    <button className="py-2 rounded-lg bg-pink-100 text-pink-700 text-sm">Chocolate</button>
                    <button className="py-2 rounded-lg bg-pink-100 text-pink-700 text-sm">Ice cream</button>
                    <button className="py-2 rounded-lg bg-pink-100 text-pink-700 text-sm">Movie night</button>
                    <button className="py-2 rounded-lg bg-pink-100 text-pink-700 text-sm">Walk together</button>
                  </div>
                </div>

                {/* Letter */}
                <div id="letter" className="mt-4 p-4 rounded-lg bg-pink-50 border border-pink-100">
                  <p className="text-sm text-pink-700 font-semibold">A little note</p>
                  <div className="mt-2 text-pink-700">
                    {letterLines.map((l,i)=> (
                      <p key={i} className="text-sm">{l}</p>
                    ))}
                  </div>
                  <p className="text-xs mt-3 text-pink-400">— {senderName}</p>
                </div>

              </div>

              {/* Footer actions */}
              <div className="mt-4 flex gap-3">
                <a href="#" onClick={(e)=>{e.preventDefault(); window.print()}} className="flex-1 text-center py-2 rounded-lg bg-white border border-pink-200 text-pink-600">Save / Print</a>
                <a href="#" onClick={(e)=>{e.preventDefault(); alert('You can add a secret URL or action here')}} className="flex-1 text-center py-2 rounded-lg bg-pink-500 text-white">Secret</a>
              </div>

            </motion.div>
          )}
        </div>

        {/* Small footer: instructions for QR usage */}
        <div className="mt-6 text-xs text-pink-400">
          Tip: Deploy this page to Vercel and share the URL. Generate a QR code from the URL and send it—when {recipientName} scans it, this page will open.
        </div>

      </div>
    </div>
  )
}

/*
Deployment steps & quick personalization checklist (include in your repo README):
1) Replace the image placeholders in `public/images/`:
   - hellokitty-icon.png (small logo)
   - kitty-sticker.png (cute sticker)
   - sample1.jpg, sample2.jpg, sample3.jpg (your photos)
2) Edit `recipientName`, `senderName`, `heroMessage`, and `letterLines` inside the file.
3) Commit & push to GitHub.
4) Go to https://vercel.com/new and import the repo. Use default settings for Next.js.
5) Once deployed, copy the production URL (e.g. https://your-app.vercel.app).
6) Go to any free QR generator (search "free qr code generator"), paste the URL and get a PNG/SVG QR.
7) Send the QR to Keshav — when he scans, the interactive Hello Kitty page opens.

Optional enhancements (I can help add any of these):
- Audio autoplay (a short song when the page opens) — note: browsers may block autoplay; better add a play button.
- Hidden message that appears after a passcode or after doing the quiz.
- Animated confetti when opened (use a lightweight confetti library).
- Small form to collect a tiny reply from Keshav ("Type your name") and show a cheeky response.
- Custom domain instead of vercel.app.

If you want, tell me the photos and the exact letter/message and I will update the code with them and give you a ready-to-deploy repo structure.
*/
