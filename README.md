# Herd Mentality (online answer sheet)

A single-page site for playing the party game **Herd Mentality** with friends over a video call. The host opens a room and reads a question, everyone types a secret answer on their phone, and the host reveals and scores once the whole herd is in.

**Live site:** https://everix1992.github.io/HerdMentality/

## How a game night works

1. The host opens the site, clicks **Open the paddock**, and shares the room code (or the copy link).
2. Friends open the site, type the code and their name, and tap **Join the herd**.
3. The host types a question (or reads one from the deck) and sends it. Everyone answers; the host sees who is in but not what they wrote.
4. **Reveal answers** groups matching answers. Tap two cards to merge answers that mean the same thing, then **Award cows**.
5. The scoreboard tracks cows, the Pink Cow, and the winning target (8, or 9 if two players hit 8 in the same round).

## How it works

- One `index.html`, no build step, no backend.
- The host's browser is the game server. Players connect to it over WebRTC data channels using [PeerJS](https://peerjs.com/) and its free public signalling server. The room code is the PeerJS id (`herd-CODE`).
- The host's game state is saved in `localStorage`, so refreshing the host tab offers **Resume game**. Players reconnect automatically.
- Only STUN is configured. If someone on a strict network (some mobile carriers, offices) can never connect, add TURN servers to `TURN_SERVERS` at the top of the script. A free [Metered](https://www.metered.ca/) account provides them.

## Rules in brief

Everyone writes the answer they think most other people will write. Everyone in the most popular group earns a cow; a tie for most popular means no cows. If exactly one player's answer matched nobody, they take the Pink Cow, and whoever holds it cannot win. First to 8 cows without the Pink Cow wins.

Rules summarised from the publisher's [how-to-play guide](https://bigpotato.com/blogs/how-to-play/herd-mentality). This is an unofficial fan project and ships none of the card text.
