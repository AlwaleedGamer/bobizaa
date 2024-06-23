import { stringify } from 'flatted';

const handler = async (m, { match, usedPrefix, noPrefix, _args, args, command, text, conn, participants, groupMetadata, user, bot, isROwner, isOwner, isRAdmin, isAdmin, isBotAdmin, isPrems, chatUpdate, __dirname, __filename }) => {

  function output(msg) {
    if (typeof msg === "number" || typeof msg === "boolean" || typeof msg === "function") {
      msg = msg.toString();
    } else if (msg instanceof Map) {
      let texte = `Map(${msg.size}) `;
      texte += JSON.stringify(mapToObj(msg), null, 2);
      msg = texte;
    } else if (typeof msg === "object") {
      try {
        msg = JSON.stringify(msg, getCircularReplacer(), 2);
      } catch (e) {
        msg = "Error converting object to string";
      }
    } else if (typeof msg === "undefined") {
      msg = "undefined";
    }

    m.reply(msg);
  }

  function out(msg) {
    output(msg);
  }

  function mapToObj(map) {
    const obj = {};
    map.forEach((v, k) => {
      obj[k] = v;
    });
    return obj;
  }

  function getCircularReplacer() {
    const seen = new WeakSet();
    return (key, value) => {
      if (typeof value === "object" && value !== null) {
        if (seen.has(value)) {
          return;
        }
        seen.add(value);
      }
      return value;
    };
  }

  if (!text) {
    return m.reply('يرجى تقديم نص لتقييمه.');
  }

  const cmd = `
    (async () => {
      try {
        ${text}
      } catch (err) {
        console.log(err);
      }
    })();`;

  try {
    eval(cmd);
  } catch (err) {
    m.reply(`*『💔』حدث خطأ أثناء تنفيذ الامر سنباي『💔』*\n\n${err}`);
  }
};

handler.help = ['eval'];
handler.tags = ['owner'];
handler.owner = true;
handler.author = "Yamada Mk";
handler.command = /^(eval)$/i;

export default handler;
