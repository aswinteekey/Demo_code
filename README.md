# Demo_code
Nothing here...


import React, { useState } from 'react';
import nlp from 'compromise';

const SentenceResponder = () => {
  const [sentence, setSentence] = useState('');
  const [response, setResponse] = useState('');

  // Step 1: Map of keywords to replies
  const keywordReplies = {
    teacher: "Teaching is a noble profession!",
    doctor: "Doctors save lives every day.",
    engineer: "Engineers build the future.",
    programmer: "Coding is like magic for machines!",
    love: "Love is the strongest force in the universe.",
    freedom: "Freedom is everyone's right."
  };

  const analyzeSentence = () => {
    const doc = nlp(sentence);
    const nouns = doc.nouns().out('array').map(n => n.toLowerCase());

    // Step 2: Find matching keyword
    const matchedKeyword = nouns.find(noun => Object.keys(keywordReplies).includes(noun));

    if (matchedKeyword) {
      setResponse(keywordReplies[matchedKeyword]);
    } else {
      setResponse("I couldn't quite get that. Can you rephrase?");
    }
  };

  return (
    <div style={{ padding: '20px', maxWidth: '600px' }}>
      <h3>Chat with Meaning Detector</h3>
      <input
        type="text"
        value={sentence}
        onChange={(e) => setSentence(e.target.value)}
        placeholder="Type something..."
        style={{ width: '100%', padding: '8px' }}
      />
      <button onClick={analyzeSentence} style={{ marginTop: '10px' }}>
        Send
      </button>

      {response && (
        <div style={{ marginTop: '20px', background: '#eee', padding: '15px', borderRadius: '10px' }}>
          <strong>Bot:</strong> {response}
        </div>
      )}
    </div>
  );
};

export default SentenceResponder;
