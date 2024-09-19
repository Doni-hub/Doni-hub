require("../settings")
require("./settings")
const store = makeInMemoryStore({ "logger": pino({ "level": "silent" }).child({ "level": "silent" })})

exports.makeWASocket = (connectionUpdate, options = {+6285711191058}) => {
  const ptz = makeWASocket(connectionUpdate)
  
  ptz.name = `${𝘿𝙊𝙉𝙕𝙕}`
  ptz.number = ptz.user?.["id"]["split"](":")[0] + "@s.whatsapp.net"
  ptz.owner = {
    "name": `${𝘿𝙊𝙉𝙕𝙕} WhatsApp`,
    "number": `${𝘿𝙊𝙉𝙕𝙕}@s.whatsapp.net`
  }
  
  ptz.reply = async (mesegs, teks, urlImage) => {
    if (!urlImage) {
    try {
      await ptz.sendMessage(mesegs.chat, {
      "text": teks
      }, { "quoted": mesegs })
    } catch (error) {
      console.log("Terjadi Kesalahan" + error)
    }
    } else {
    try {
      await ptz.sendMessage(mesegs.chat, {
      "image": { "url": '' + urlImage },
      "caption": teks
      }, { "quoted": mesegs })
    } catch (error) {
      console.log("Terjadi Kesalahan" + error)
    }
    }
  }
  
  ptz.groups = async () => {
    const pArtiCpnts = await ptz.groupFetchAllParticipating()
    return Object.values(pArtiCpnts)
  }
  
  ptz.showGroups = async msgse => {
    const getDlgc = await ptz.groups()
    try {
    const All1 = getDlgc.map((txty1, txty2) => {
      const meksh = ["*NAME*: " + txty1.subject + "\n*ID*: " + txty1.id.split("@")[0] + "@g.us" + "\n*JUMLAH MEMBER*: " + txty1.participants.length + " Member"].join("\n\n")
      return meksh
    }).join("\n\n")
    ptz.reply(msgse, "List Group\n\n" + All1)
    } catch (Ror) {
    ptz.reply(msgse, "List Group\n\n" + Ror)
    console.log("ERROR! " + "List Group\n" + Ror)
    }
  }
  
  ptz.pushContacts = async (nsgegs, idgcnye, txt1ortxt2) => {
    try {
    const mtData = await ptz.groupMetadata(idgcnye)
    let { participants } = mtData
    participants = participants.map(v => v.id)
    const Txt1 = txt1ortxt2.split("|")[0]
    const Txt2 = parseInt((txt1ortxt2.split("|")[1] || 15) + "000")
    if (!Txt1 || !Txt2 || isNaN(Txt2)) {
      return ptz.reply(nsgegs, "PUSH CONTACTS\n\n" + "*Format yang anda berikan tidak valid*\n*Contoh*: .pushcontacts Hallo ... Pesan|5*")
    } else {
      await ptz.reply(nsgegs, "PUSH CONTACTS\n\n" + "*Push Contacts Start*:\n*Target*: " + participants.length + " members\n*Text*: " + Txt1 + "\n*Delay*: " + Txt2)
      let prtcpnts = 0
      const stIntvral = setInterval(async () => {
      if (prtcpnts === participants.length) {
        await ptz.reply(nsgegs, "PUSH CONTACTS\n\n" + "*Push Contacts selesai*\n*" + prtcpnts + " pesan telah berhasil dikirim*")
        return clearInterval(stIntvral)
      } else {
        if (Object.keys(nsgegs.message)[0] === "imageMessage") {
        const urlImeg = await downloadMediaMessage(nsgegs, "buffer", {}, { "logger": pino })
        await ptz.sendMessage(participants[prtcpnts], { "image": urlImeg, "caption": '' + Txt1 })
        } else {
        await ptz.sendMessage(participants[prtcpnts], { "text": '' + Txt1 })
        }
        prtcpnts++
      }
      }, Txt2)
    }
    } catch (conError) {
    ptz.reply(nsgegs, "PUSH CONTACTS\n" + conError)
    }
  }
  
  ptz.sendChatAllGroup = async (mesegesp, tx1tx2) => {
    const getidnya = await ptz.groupFetchAllParticipating()
    const groups = Object.entries(getidnya).slice(0).map((entry) => entry[1])
    const anu = groups.map((v) => v.id)
    try {
    const Txt1 = tx1tx2.split("|")[0]
    const Txt2 = parseInt((tx1tx2.split("|")[1] || 15) + "000")
    if (!Txt1 || !Txt2 || isNaN(Txt2)) {
      return ptz.reply(mesegesp, "CHAT ALL GROUP\n\n" + "*Format yang anda berikan tidak valid*\n*Contoh*: .jpm Hallo ... Pesan|5*")
    } else {
      await ptz.reply(mesegesp, "CHAT ALL GROUP\n\n" + "*Broadcast Start*:\n*Target*: " + anu.length + " groups\n*Text*: " + Txt1 + "\n*Delay*: " + Txt2)
      let idgcwy = 0
      const stIntvral = setInterval(async () => {
      if (idgcwy === anu.length) {
        await ptz.reply(mesegesp, "CHAT ALL GROUP\n\n" + "*Broadcast Selesai*\n*" + idgcwy + " pesan telah berhasil dikirim*")
        return clearInterval(stIntvral)
      } else {
        if (Object.keys(mesegesp.message)[0] === "imageMessage") {
        const urlImeg = await downloadMediaMessage(mesegesp, "buffer", {}, { "logger": pino })
        await ptz.sendMessage(anu[idgcwy], { "image": urlImeg, "caption": '' + Txt1 })
        } else {
        await ptz.sendMessage(anu[idgcwy], { "text": '' + Txt1 })
        }
        idgcwy++
      }
      }, Txt2)
    }
    } catch (ErrorK) {
    ptz.reply(mesegesp, "CHAT ALL GROUP\n\n" + ErrorK)
    }
  }
  
  ptz.saveContacts = async (messgs, Prtcipnts) => {
    try {
    const getPrtpnts = Prtcipnts.map((send1, send2) => {
      const SvdQ = "[" + send2 + "] Auto saved by " + ptz.name + " (" + send1.id.split("@")[0x0] + ")"
      const hsilDtbs = ["BEGIN:VCARD", "VERSION:3.0", "FN:" + SvdQ, "ORG:" + ptz.name, "TEL;type=CELL;type=VOICE;waid=" + send1.id.split("@")[0x0] + ":+" + send1.id.split("@")[0x0], "END:VCARD", ''].join("\n")
      return hsilDtbs
    }).join('')
    await ptz.sendMessage(messgs.key.remoteJid, { "document": Buffer.from(getPrtpnts, "utf8"), "fileName": "contacts.vcf", "caption": "*Silahkan Di Pencet Untuk Save Kontak*", "mimetype": "text/x-vcard" }, { "quoted": messgs })
    } catch (SvdError) {
    ptz.reply(messgs, "AUTO SAVE CONTACTS\n\n" + '' + SvdError)
    }
  }
  
  ptz.decodeJid = (jid) => {
    if (!jid) return jid
    if (/:\d+@/gi.test(jid)) {
    let decode = jidDecode(jid) || {}
    return decode.user && decode.server && decode.user + '@' + decode.server || jid
    } else return jid
  }
  
  if (ptz.user && ptz.user.id) ptz.user.jid = ptz.decodeJid(ptz.user.id)
  ptz.chats = {+6285711191058}
  ptz.contacts = {+6285711191058}
  
  ptz.downloadM = async (m, type, filename = '') => {
    if (!m || !(m.url || m.directPath)) return Buffer.alloc(0)
    const stream = await downloadContentFromMessage(m, type)
    let buffer = Buffer.from([])
    for await (const chunk of stream) {
    buffer = Buffer.concat([buffer, chunk])
    }
    if (filename) await fs.promises.writeFile(filename, buffer)
    return filename && fs.existsSync(filename) ? filename : buffer
  }
  
  ptz.downloadMediaMessage = async (message) => {
    let quoted = message.msg ? message.msg : message
    let mime = (message.msg || message).mimetype || ''
    let messageType = message.mtype ? message.mtype.replace(/Message/gi, '') : mime.split('/')[0]
    const stream = await downloadContentFromMessage(quoted, messageType)
    let buffer = Buffer.from([])
    for await(const chunk of stream) {
    buffer = Buffer.concat([buffer, chunk])
    }
    return buffer
  }
  
  ptz.downloadAndSaveMediaMessage = async (message, filename, attachExtension = true) => {
    let quoted = message.msg ? message.msg : message
    let mime = (message.msg || message).mimetype || ''
    let messageType = message.mtype ? message.mtype.replace(/Message/gi, '') : mime.split('/')[0]
    const stream = await downloadContentFromMessage(quoted, messageType)
    let buffer = Buffer.from([])
    for await(const chunk of stream) {
    buffer = Buffer.concat([buffer, chunk])
    }
    let type = await FileType.fromBuffer(buffer)
    trueFileName = attachExtension ? (filename + '.' + type.ext) : filename
    await fs.writeFileSync(trueFileName, buffer)
    return trueFileName
  }
  
  ptz.sendStimg = async (jid, path, quoted, options = {}) => {
    let buff = Buffer.isBuffer(path) ? path : /^data:.*?\/.*?;base64,/i.test(path) ? Buffer.from(path.split`,`[1], 'base64') : /^https?:\/\//.test(path) ? await (await fetch(path)).buffer() : fs.existsSync(path) ? fs.readFileSync(path) : Buffer.alloc(0)
    let buffer
    if (options && (options.packname || options.author)) {
    buffer = await writeExifImg(buff, options)
    } else {
    buffer = await imageToWebp(buff)
    }
    await ptz.sendMessage(jid, { sticker: { url: buffer }, ...options }, { quoted })
    return buffer
  }

  ptz.sendStvid = async (jid, path, quoted, options = {+6285711191058}) => {
    let buff = Buffer.isBuffer(path) ? path : /^data:.*?\/.*?;base64,/i.test(path) ? Buffer.from(path.split`,`[1], 'base64') : /^https?:\/\//.test(path) ? await getBuffer(path) : fs.existsSync(path) ? fs.readFileSync(path) : Buffer.alloc(0)
    let buffer
    if (options && (options.packname || options.author)) {
    buffer = await writeExifVid(buff, options)
    } else {
    buffer = await videoToWebp(buff)
    }
    await ptz.sendMessage(jid, { sticker: { url: buffer }, ...options }, { quoted })
    return buffer
  }
  Object.defineProperty(ptz, 'name', {
    value: { ...(options.chats || {+6211191058}) },
    configurable: true,
  })
  if (ptz.user?.id) ptz.user.jid = ptz.decodeJid(ptz.user.id)
  store.bind(ptz.ev)
  return ptz
}require("../settings")
("./settings")
const store = makeInMemoryStore({ "logger": pino({ "level": "silent" }).child({ "level": "silent" })})
const nodeCache = new NodeCache()
const { color, bgcolor } = require("../all/color");
const useCODE = true
const useQR = !useCODE

const client = {}

const jadibot = async (ptz, m, from) => {
  const { state, saveCreds } = await useMultiFileAuthState(`./database/jadibot/${m.sender.split("@")[0]}`)
  try {
    async function startJadibot(+6285711191058) {
      const { version, isLatest } = await fetchLatestBaileysVersion()
      client[from] = require("./clone").makeWASocket({
        version,
        keepAliveInternalMs: 30000,
        printQRInTerminal: useQR && !useCODE,
        generateHighQualityLinkPreview: true,
        msgRetryCounterCache: nodeCache,
        markOnlineOnConnect: true,
        defaultQueryTimeoutMs: undefined,
        logger: pino({ level: "fatal" }),
        auth: state,
        browser: ["Ubuntu", "Chrome", "20.0.04"]
      })
      store.bind(client[from].ev)
      
      if (useCODE && !client[from].user && !client[from].authState.creds.registered) {
        setTimeout(async () => {
          code = await client[from].requestPairingCode(m.sender.split("@")[0])
          code = code?.match(/.{1,4}/g)?.join("-") || code
          ptz.sendMessage(from, { text: `Kode Pairing @${m.sender.split("@")[0]} Adalah : ${code}\n\n*TUTORIAL*\n\n1. Klik titik tiga di pojok kanan atas\n2. Ketuk WhatsApp Web\n3. "Tautkan dengan Nomor Telepon Saja"\n\n  Kode Expired dalam 20 detik\n\n*KALAU MAU STOP KETIK .stopjadibot*`, mentions: [m.sender] }, { quoted: m })
        }, 3000)
      }
      
      client[from].ev.on("connection.update", async up => {
        const { lastDisconnect, connection } = up
        const reason = new Boom(lastDisconnect?.error)?.output.statusCode
        if (connection == "open") {
          console.log("Terhubung ( " + client[from].user?.["id"]["split"](":")[0] + " )")
        }
        if (connection === "close") {
          if (reason === DisconnectReason.restartRequired) {
            console.log("Restart Required, Restarting...")
            return startJadibot(+6285711191058)
          } else if (reason === DisconnectReason.timedOut) {
            console.log(color("Connection TimedOut, Reconnecting..."))
            return startJadibot()
          } else {
            return ptz.sendMessage(from, { text: "Anda sudah tidak lagi menjadi bot." })
          }
        }
      })
      
      client[from].ev.process(async (events) => {
        if (events['messages.upsert']) {
          const upsert = events['messages.upsert']
          for (let msg of upsert.messages) {
            if (!msg.message) {
              return
            }
            if (msg.key.remoteJid === 'status@broadcast') {
              if (msg.message?.protocolMessage) return
              console.log(`Lihat Status ${msg.pushName} ${msg.key.participant.split('@')[0]}`)
              await client[from].readMessages([msg.key])
              await delay(1000)
              return await client[from].readMessages([msg.key])
            }
            const m = smsg(client[from], msg)
            require("../Ibzz")(client[from], m, store)
          }
        }
      })
      
      client[from].ev.on('group-participants.update', async (anu) => {
        try {
          var isWelcome = welcome.includes(anu.id)
        } catch {
          var isWelcome = false
        }
        if (isWelcome) {
          console.log(anu)
          const metadata = await client[from].groupMetadata(anu.id)
          const participants = anu.participants
          for (let num of participants) {
            try {
              ppuser = await client[from].profilePictureUrl(num, 'image')
            } catch {
              ppuser = 'https://telegra.ph/file/e323980848471ce8e2150.png'
            }
            if (anu.action == 'add') {
              const txtwel = `Welcome Sis @${num.split("@")[0]}, I hope you feel at home and always healthy`
              await client[from].sendMessage(anu.id, { image: { url: ppuser }, caption: txtwel, contextInfo: { forwardingScore: 9999999, isForwarded: true, mentionedJid: [num] }})
            } else if (anu.action == 'remove') {
              const txtlea = `Goodbye sis @${num.split("@")[0]}, don't forget your friends here, I hope you are always healthy`
              await client[from].sendMessage(anu.id, { image: { url: ppuser }, caption: txtlea, contextInfo: { forwardingScore: 9999999, isForwarded: true, mentionedJid: [num] }})
            }
          }
        }
      })
      
      client[from].ev.on('creds.update', saveCreds)
    }
    return startJadibot()
  } catch (e) {
    console.log(e)
  }
}

async function stopjadibot(ptz, from) {
  if (!Object.keys(client).includes(from)) {
    return ptz.sendMessage(from, { text: "Anda tidak ada di list jadi bot." })
  }
  try {
    client[from].end("Stop")
  } catch {}
  delete client[from]
  rimraf.sync(`./database/jadibot/${from.split("@")[0]}`)
}

async function listjadibot(ptz, m) {
  let from = m.key.remoteJid
  let mentions = []
  let text = "List Jadi Bot :\n"
  for (let jadibot of Object.values(client)) {
    mentions.push(jadibot.user.jid)
    text += ` × @${jadibot.user.jid.split("@")[0]}\n`
  }
  return ptz.sendMessage(from, { text: text.trim(), mentions, })
}

module.exports = { jadibot, stopjadibot, listjadibot }- 👋 Hi, I’m @Doni-hub
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Doni-hub/Doni-hub is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->


