// POST /api/extract
// Body: { image: "<base64 string, no data: prefix>", mediaType: "image/jpeg" }
// Returns: { emri, mbiemri, ditelindje, nr_karte_identiteti, data_leshimit, data_skadence }
//
// Requires the environment variable ANTHROPIC_API_KEY to be set in your
// Vercel project settings (Project -> Settings -> Environment Variables).
// Get a key at https://console.anthropic.com/settings/keys

export default async function handler(req, res) {
  if (req.method !== 'POST') {
    res.status(405).json({ error: 'Method not allowed' });
    return;
  }

  const apiKey = process.env.ANTHROPIC_API_KEY;
  if (!apiKey) {
    res.status(500).json({ error: 'Server is missing ANTHROPIC_API_KEY' });
    return;
  }

  try {
    const { image, mediaType } = req.body || {};
    if (!image || !mediaType) {
      res.status(400).json({ error: 'Missing image or mediaType in request body' });
      return;
    }

    const systemPrompt = `You extract fields from a photo of a national ID card (Albanian or other). Respond with ONLY a raw JSON object, no markdown, no preamble, with exactly these keys: emri (first name), mbiemri (surname), ditelindje (date of birth, format DD/MM/YYYY), nr_karte_identiteti (ID card number), data_leshimit (date of issue, DD/MM/YYYY), data_skadence (date of expiry, DD/MM/YYYY). If a field is not clearly visible or you are not confident, set its value to an empty string "" rather than guessing.`;

    const anthropicRes = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': apiKey,
        'anthropic-version': '2023-06-01',
      },
      body: JSON.stringify({
        model: 'claude-sonnet-4-6',
        max_tokens: 1000,
        system: systemPrompt,
        messages: [
          {
            role: 'user',
            content: [
              { type: 'image', source: { type: 'base64', media_type: mediaType, data: image } },
              { type: 'text', text: 'Extract the fields from this ID card and return only the JSON object.' },
            ],
          },
        ],
      }),
    });

    if (!anthropicRes.ok) {
      const errText = await anthropicRes.text();
      res.status(502).json({ error: 'Anthropic API error', detail: errText });
      return;
    }

    const data = await anthropicRes.json();
    const textBlock = (data.content || []).find((b) => b.type === 'text');
    let parsed = {};
    if (textBlock) {
      const clean = textBlock.text.replace(/```json|```/g, '').trim();
      try {
        parsed = JSON.parse(clean);
      } catch (e) {
        parsed = {};
      }
    }

    res.status(200).json({
      emri: parsed.emri || '',
      mbiemri: parsed.mbiemri || '',
      ditelindje: parsed.ditelindje || '',
      nr_karte_identiteti: parsed.nr_karte_identiteti || '',
      data_leshimit: parsed.data_leshimit || '',
      data_skadence: parsed.data_skadence || '',
    });
  } catch (err) {
    res.status(500).json({ error: 'Extraction failed', detail: String(err) });
  }
}
