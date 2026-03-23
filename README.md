package com.example.toainsanity;

import com.google.inject.Provides;
import javax.inject.Inject;

import net.runelite.api.Client;
import net.runelite.api.coords.WorldPoint;
import net.runelite.api.events.GameTick;
import net.runelite.client.eventbus.Subscribe;
import net.runelite.client.plugins.Plugin;
import net.runelite.client.plugins.PluginDescriptor;
import net.runelite.client.ui.overlay.OverlayManager;

@PluginDescriptor(
    name = "ToA Insanity Helper"
)
public class ToaInsanityPlugin extends Plugin
{
    @Inject
    private Client client;

    @Inject
    private OverlayManager overlayManager;

    @Inject
    private ToaInsanityOverlay overlay;

    private WorldPoint lastTile = null;
    private WorldPoint previousTile = null;

    private int tickCounter = 0;

    @Override
    protected void startUp()
    {
        overlayManager.add(overlay);
    }

    @Override
    protected void shutDown()
    {
        overlayManager.remove(overlay);
        lastTile = null;
        previousTile = null;
    }

    @Subscribe
    public void onGameTick(GameTick event)
    {
        tickCounter++;

        // ⚠️ Esto es un placeholder:
        // Acá deberías detectar el tile golpeado por el piso (graphic/object/event real)
        WorldPoint detectedTile = detectDangerTile();

        if (detectedTile != null)
        {
            previousTile = lastTile;
            lastTile = detectedTile;
            tickCounter = 0;
        }
    }

    private WorldPoint detectDangerTile()
    {
        // TODO: lógica real (graphics objects del piso)
        return null;
    }

    public WorldPoint getLastTile()
    {
        return lastTile;
    }

    public WorldPoint getPreviousTile()
    {
        return previousTile;
    }

    public int getTickCounter()
    {
        return tickCounter;
    }
}