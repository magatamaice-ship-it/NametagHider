
package id.server.nametaghider;

import org.bukkit.Bukkit;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;
import org.bukkit.event.player.PlayerQuitEvent;
import org.bukkit.scoreboard.Scoreboard;
import org.bukkit.scoreboard.Team;
import org.bukkit.plugin.java.JavaPlugin;

public class NametagHider extends JavaPlugin implements Listener {

    private Scoreboard scoreboard;
    private Team hiddenTeam;

    @Override
    public void onEnable() {
        scoreboard = Bukkit.getScoreboardManager().getMainScoreboard();

        hiddenTeam = scoreboard.getTeam("nametaghider");
        if (hiddenTeam == null) {
            hiddenTeam = scoreboard.registerNewTeam("nametaghider");
        }

        hiddenTeam.setOption(
                Team.Option.NAME_TAG_VISIBILITY,
                Team.OptionStatus.NEVER
        );

        Bukkit.getPluginManager().registerEvents(this, this);

        for (Player player : Bukkit.getOnlinePlayers()) {
            hideNametag(player);
        }

        getLogger().info("NametagHider aktif!");
    }

    private void hideNametag(Player player) {
        player.setScoreboard(scoreboard);

        Team oldTeam = scoreboard.getEntryTeam(player.getName());
        if (oldTeam != null && oldTeam != hiddenTeam) {
            oldTeam.removeEntry(player.getName());
        }

        hiddenTeam.addEntry(player.getName());
    }

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        hideNametag(event.getPlayer());
    }

    @EventHandler
    public void onPlayerQuit(PlayerQuitEvent event) {
        hiddenTeam.removeEntry(event.getPlayer().getName());
    }
}
