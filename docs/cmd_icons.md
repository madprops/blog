# Command Icons

I gained a new trick.

I go back in shell history very often to re-run the same commands over and over.

There's no efficient way to do this yet.

I think this is a problem that needs to be solved with a specialized tool.

I might try making some shell injection using rofi later.

But for now I thought of a trick that mitigates it somewhat.

Add icons to commands, so you can instantly recognize them on up arrows:

`: "✅"; ./utils/check.sh`

`: "⚡"; ./scripts/tag.py`

`: "📚"; ./scripts/makedocs.sh`

The icons are not part of the command, they do nothing.

But now your vision recognizes the correct item very quickly.